<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const canvasRef = ref(null)
let ctx = null
let width = 0
let height = 0
let mouseX = -1000
let mouseY = -1000
let animationFrame = null
let originalImageData = null

// 初始化 Canvas
const initCanvas = () => {
  const canvas = canvasRef.value
  if (!canvas) return
  ctx = canvas.getContext('2d', { willReadFrequently: true })
  resizeCanvas()
  drawText()
  originalImageData = ctx.getImageData(0, 0, width, height)
}

const resizeCanvas = () => {
  const container = canvasRef.value.parentElement
  width = container.clientWidth
  height = container.clientHeight
  canvasRef.value.width = width
  canvasRef.value.height = height
}

const drawText = () => {
  ctx.clearRect(0, 0, width, height)
  // 调整文字颜色：浅白色偏蓝，与天蓝色背景形成柔和对比（非刺眼）
  ctx.font = '370px "Segoe UI Black"'
  ctx.fillStyle = 'rgb(250, 253, 255)' // 更浅的白，适配天蓝色背景
  ctx.textAlign = 'center'
  ctx.textBaseline = 'middle'
  ctx.fillText('SIGFLOW', width / 2, height / 2)
}

// 增强的像素效果（适配天蓝色背景）
const applyPixelEffect = () => {
  if (!ctx || !originalImageData) return

  const radius = 200 // 影响半径
  const maxShift = 25 // 最大位移
  const glowIntensity = 1.8 // 光晕强度（适配天蓝，略提高增强层次感）
  const chromaShift = 6 // RGB分离最大偏移（降低，避免色彩杂乱）

  // 仅计算受影响矩形区域，减少遍历范围
  const minX = Math.max(0, Math.floor(mouseX - radius))
  const maxX = Math.min(width, Math.ceil(mouseX + radius))
  const minY = Math.max(0, Math.floor(mouseY - radius))
  const maxY = Math.min(height, Math.ceil(mouseY + radius))

  const imageData = new ImageData(new Uint8ClampedArray(originalImageData.data), width, height)
  const data = imageData.data
  const originalData = originalImageData.data

  // 遍历受影响矩形内的每个像素
  for (let y = minY; y < maxY; y++) {
    for (let x = minX; x < maxX; x++) {
      const dx = mouseX - x
      const dy = mouseY - y
      const distance = Math.sqrt(dx * dx + dy * dy)

      if (distance < radius) {
        // 计算归一化距离 (0~1)
        const t = distance / radius
        // 扭曲强度：非线性，越近越大
        const strength = (1 - t * t) * maxShift
        // 方向：像素远离鼠标
        const angle = Math.atan2(dy, dx)
        const shiftX = Math.round(Math.cos(angle) * strength)
        const shiftY = Math.round(Math.sin(angle) * strength)

        // 基础采样坐标
        let srcX = x + shiftX
        let srcY = y + shiftY
        srcX = Math.min(width - 1, Math.max(0, srcX))
        srcY = Math.min(height - 1, Math.max(0, srcY))
        const srcIndex = (srcY * width + srcX) * 4

        // 光晕：适配天蓝色背景，调整光晕因子（偏冷色调）
        const glowFactor = 1 + (1 - t) * (glowIntensity - 1)

        // RGB分离：适配天蓝背景，调整偏移方向和强度，偏向蓝系
        // 红色通道：弱偏移（避免红配蓝刺眼）
        const redShiftX = Math.round(Math.cos(angle) * chromaShift * t * 0.5)
        const redShiftY = Math.round(Math.sin(angle) * chromaShift * t * 0.5)
        let redSrcX = Math.min(width - 1, Math.max(0, srcX + redShiftX))
        let redSrcY = Math.min(height - 1, Math.max(0, srcY + redShiftY))
        const redIndex = (redSrcY * width + redSrcX) * 4

        // 绿色通道：微偏移（中和天蓝的冷感）
        const greenShiftX = Math.round(Math.cos(angle + Math.PI) * chromaShift * t * 0.4)
        const greenShiftY = Math.round(Math.sin(angle + Math.PI) * chromaShift * t * 0.4)
        let greenSrcX = Math.min(width - 1, Math.max(0, srcX + greenShiftX))
        let greenSrcY = Math.min(height - 1, Math.max(0, srcY + greenShiftY))
        const greenIndex = (greenSrcY * width + greenSrcX) * 4

        // 蓝色通道：主偏移（强化天蓝背景融合度）
        const blueShiftX = Math.round(Math.cos(angle + Math.PI / 2) * chromaShift * t * 0.8)
        const blueShiftY = Math.round(Math.sin(angle + Math.PI / 2) * chromaShift * t * 0.8)
        let blueSrcX = Math.min(width - 1, Math.max(0, srcX + blueShiftX))
        let blueSrcY = Math.min(height - 1, Math.max(0, srcY + blueShiftY))
        const blueIndex = (blueSrcY * width + blueSrcX) * 4

        const dstIndex = (y * width + x) * 4

        // 合并通道并应用光晕，限制RGB最大值避免过曝
        data[dstIndex] = Math.min(255, Math.max(0, originalData[redIndex] * glowFactor * 0.95)) // 红通道弱化
        data[dstIndex + 1] = Math.min(
          255,
          Math.max(0, originalData[greenIndex] * glowFactor * 1.05),
        ) // 绿通道微调
        data[dstIndex + 2] = Math.min(255, Math.max(0, originalData[blueIndex] * glowFactor * 1.1)) // 蓝通道强化（适配背景）
        data[dstIndex + 3] = originalData[srcIndex + 3] // Alpha 不变
      } else {
        // 区域外直接复制原始像素
        const index = (y * width + x) * 4
        data[index] = originalData[index]
        data[index + 1] = originalData[index + 1]
        data[index + 2] = originalData[index + 2]
        data[index + 3] = originalData[index + 3]
      }
    }
  }

  ctx.putImageData(imageData, 0, 0)
}

// 鼠标移动处理（节流）
const handleMouseMove = (e) => {
  const rect = canvasRef.value.getBoundingClientRect()
  mouseX = e.clientX - rect.left
  mouseY = e.clientY - rect.top
  mouseX = Math.min(width, Math.max(0, mouseX))
  mouseY = Math.min(height, Math.max(0, mouseY))

  if (!animationFrame) {
    animationFrame = requestAnimationFrame(() => {
      applyPixelEffect()
      animationFrame = null
    })
  }
}

const handleMouseLeave = () => {
  mouseX = -1000
  mouseY = -1000
  drawText()
}

const handleResize = () => {
  resizeCanvas()
  drawText()
  originalImageData = ctx.getImageData(0, 0, width, height)
}

onMounted(() => {
  initCanvas()
  window.addEventListener('resize', handleResize)
})

onUnmounted(() => {
  window.removeEventListener('resize', handleResize)
  if (animationFrame) {
    cancelAnimationFrame(animationFrame)
  }
})
</script>

<template>
  <div class="sigflow">
    <canvas ref="canvasRef" @mousemove="handleMouseMove" @mouseleave="handleMouseLeave"></canvas>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  list-style: none;
}

.sigflow {
  /* 移除 fixed 定位，改为普通块级元素 */
  width: 100%;
  height: 370px;
  background-color: #87ceeb; /* 天蓝色背景，可按需调整 */
  cursor: default;
  /* 如果希望底部栏与上方内容紧贴，可添加 margin-top: 0 等 */
}

canvas {
  display: block;
  width: 100%;
  height: 100%;
  background: transparent;
}
</style>
