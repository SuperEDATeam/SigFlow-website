<script setup>
import { ref, computed } from 'vue'

// 三个图标的图片路径（请根据实际路径调整）
import icon1 from '../../assets/images/Panel/icon1.png'
import icon2 from '../../assets/images/Panel/icon2.png'
import icon3 from '../../assets/images/Panel/icon3.png'

// 右侧展示的图片路径
import pannel1 from '../../assets/images/Panel/pannel1.png'
import pannel2 from '../../assets/images/Panel/pannel2.png'
import pannel3 from '../../assets/images/Panel/pannel3.png'

// 面板数据结构：标题 + 内容
const panels = [
  {
    title: '项目资源管理器面板',
    content:
      '项目资源管理器。用于显示、组织和配置SigFlow项目的文件资源，包括src/(存储源码)、lib/(存储库代码)、project.sigflow(项目配置文件)、.sigflow/(存储画布数据、仿真数据等)、.cache/(存储软件运行所需要暂存的临时文件)',
  },
  {
    title: 'SigFlow Tree面板',
    content:
      'SigFlow Tree面板。用于显示软件的核心数据SFTree，层次从上到下依次为项目、文件、顶层模块、模块内的实现',
  },
  {
    title: '元件库面板',
    content:
      '元件库面板。用于显示和选择画布上绘制的元件类型，包括输入输出、布线部件、元件门、语法块和自定义模块。双击即可拖动到画布放置',
  },
]

const activeIndex = ref(0)
const currentImage = computed(() => {
  const images = [pannel1, pannel2, pannel3]
  return images[activeIndex.value]
})
const currentPanel = computed(() => panels[activeIndex.value])

const setActive = (index) => {
  activeIndex.value = index
}

// ---------- 提示框逻辑（允许超出父容器右侧，但限制左侧和上下）----------
const showTooltip = ref(false)
const tooltipX = ref(0)
const tooltipY = ref(0)

const rightRef = ref(null)
const tooltipRef = ref(null)

const updatePosition = (event) => {
  if (!rightRef.value) return

  const rect = rightRef.value.getBoundingClientRect()
  const mouseX = event.clientX - rect.left
  const mouseY = event.clientY - rect.top

  let tooltipWidth = 80
  let tooltipHeight = 30
  if (tooltipRef.value) {
    tooltipWidth = tooltipRef.value.offsetWidth
    tooltipHeight = tooltipRef.value.offsetHeight
  }

  let left = mouseX + 15
  let top = mouseY + 20

  // 左侧边界限制
  if (left < 0) {
    left = Math.max(5, mouseX + 5)
  }
  // 右侧允许超出，但防止超出视口
  const viewportWidth = window.innerWidth
  const rightEdge = left + tooltipWidth
  if (rightEdge > viewportWidth - 10) {
    left = viewportWidth - tooltipWidth - 10
  }
  if (left < 5) left = 5

  // 上下边界限制
  if (top + tooltipHeight > rect.height) {
    top = mouseY - tooltipHeight - 20
  }
  if (top < 0) {
    top = Math.max(5, mouseY + 5)
  }
  top = Math.min(Math.max(top, 2), rect.height - tooltipHeight - 2)

  tooltipX.value = left
  tooltipY.value = top
}

const handleMouseEnter = (event) => {
  showTooltip.value = true
  updatePosition(event)
  import('vue').then(({ nextTick }) => {
    nextTick(() => {
      if (showTooltip.value) updatePosition(event)
    })
  })
}

const handleMouseMove = (event) => {
  if (showTooltip.value) updatePosition(event)
}

const handleMouseLeave = () => {
  showTooltip.value = false
}
</script>

<template>
  <div class="leftbar">
    <div class="left">
      <ul>
        <li
          v-for="(icon, index) in [icon1, icon2, icon3]"
          :key="index"
          :class="{ active: activeIndex === index }"
          @click="setActive(index)"
        >
          <img :src="icon" alt="icon" />
        </li>
      </ul>
    </div>

    <div class="right" ref="rightRef">
      <img
        :src="currentImage"
        alt="panel"
        class="panel-image"
        @mouseenter="handleMouseEnter"
        @mousemove="handleMouseMove"
        @mouseleave="handleMouseLeave"
      />

      <div
        v-show="showTooltip"
        ref="tooltipRef"
        class="tooltip"
        :style="{ left: tooltipX + 'px', top: tooltipY + 'px' }"
      >
        <div class="tooltip-title">{{ currentPanel.title }}</div>
        <div class="tooltip-content">{{ currentPanel.content }}</div>
      </div>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  list-style: none;
  box-sizing: border-box;
}

.leftbar {
  position: absolute;
  left: 0;
  top: 5%;
  width: 14%;
  height: 95%;
  background-color: #ffffff;
  display: flex;
  flex-direction: row;
  box-shadow: 2px 0 8px rgba(0, 0, 0, 0.02);
}

.leftbar .left {
  width: 20%;
  height: 100%;
  background-color: #f8f9fa;
  border-right: 1px solid #eaeef2;
}

.leftbar .left ul {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 20px;
}

.leftbar .left li {
  width: 100%;
  aspect-ratio: 1 / 1;
  margin: 8px 0;
  cursor: pointer;
  border: 2px solid transparent;
  transition: border-color 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 6px;
}

.leftbar .left li.active {
  border-color: #3b82f6;
  background-color: rgba(59, 130, 246, 0.04);
}

.leftbar .left li img {
  width: 70%;
  height: auto;
  max-height: 70%;
  object-fit: contain;
  display: block;
}

.leftbar .right {
  position: relative;
  background-color: #ffffff;
  flex: 1;
}

.panel-image {
  width: 100%;
  height: 100%;
  object-fit: contain;
  display: block;
  background-color: inherit;
}

.tooltip {
  position: absolute;
  background-color: rgba(230, 242, 255, 0.95);
  color: #1e2a3a;
  border-radius: 8px;
  border: 1px solid #b8d9ff;
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.1);
  padding: 8px 12px;
  width: 280px;
  height: 160px;
  overflow-y: auto;
  pointer-events: none;
  z-index: 1000;
  backdrop-filter: blur(4px);
  font-family:
    system-ui,
    -apple-system,
    'Segoe UI',
    Roboto,
    sans-serif;
  line-height: 1.4;
  white-space: normal;
  word-wrap: break-word;
  word-break: break-word;
}

.tooltip-title {
  font-weight: 700;
  font-size: 14px;
  color: #0f3b5c;
  margin-bottom: 6px;
  border-left: 3px solid #3b82f6;
  padding-left: 8px;
  letter-spacing: 0.3px;
}

.tooltip-content {
  font-weight: 400;
  font-size: 12px;
  color: #2c3e50;
  line-height: 1.45;
  text-align: left;
  word-break: break-word;
}

.tooltip::-webkit-scrollbar {
  width: 4px;
}
.tooltip::-webkit-scrollbar-track {
  background: #e2e8f0;
  border-radius: 4px;
}
.tooltip::-webkit-scrollbar-thumb {
  background: #94a3b8;
  border-radius: 4px;
}
</style>
