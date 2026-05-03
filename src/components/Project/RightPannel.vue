<script setup>
import { ref, nextTick, onUnmounted } from 'vue'

// 介绍内容数组，顺序对应九个盒子（每个对象包含标题和内容）
const introductions = [
  {
    title: '项目管理按钮组',
    content: '1. 新建项目 2. 打开项目 3. 保存项目',
  },
  {
    title: '编辑按钮组',
    content: '撤回：撤回到上一次的编辑操作，包括画布编辑和Verilog编辑在内的所有电路设计操作',
  },
  {
    title: '验证按钮组',
    content: '5. 开始仿真 6. 终止仿真',
  },
  {
    title: '新建模块',
    content: '+ : 用于新建画布标签页，即新建一个Verilog模块',
  },
  {
    title: '画布',
    content:
      '用于绘制电路原理图，一个画布标签页代表一个模块。在画布上，可以进行画布拖动、元件放置/删除、元件标识符/位置编辑、导线绘制等编辑操作。在仿真验证阶段可以将各个信号的值直观表示出来',
  },
  {
    title: '画布元件',
    content:
      '画布的绘制单元，显示的内容包括元件标识符，元件引脚，引脚的标识符。元件的样式可以自定义，单击选中元件后，可以在右侧侧边栏对其进行编辑',
  },
  {
    title: 'Verilog编辑器',
    content: '用于编辑Verilog代码。具有行号显示，静态检测，语法块检测等IDE级功能',
  },
  {
    title: '输出面板',
    content: '包括终端和波形图面板。终端用于命令交互，软件状态输出。波形图面板用于离线仿真波形显示',
  },
  {
    title: '右侧侧边栏',
    content:
      '提供属性栏用于编辑元件/导线的各种信息，包括标识符，输入输出引脚的标识符，各个引脚的连接信号等等',
  },
]

// 提示框状态
const showTooltip = ref(false)
const tooltipContent = ref({ title: '', content: '' })
const tooltipX = ref(0)
const tooltipY = ref(0)

const rightRef = ref(null)
const tooltipRef = ref(null)

// 定时器与动画句柄
let leaveTimer = null
let rafId = null

// 更新提示框位置（使用 requestAnimationFrame 节流）
const updatePosition = (event) => {
  if (!rightRef.value) return
  if (rafId) cancelAnimationFrame(rafId)
  rafId = requestAnimationFrame(() => {
    try {
      const rect = rightRef.value.getBoundingClientRect()
      const mouseX = event.clientX - rect.left
      const mouseY = event.clientY - rect.top

      // 获取提示框真实尺寸
      const tooltipEl = tooltipRef.value
      let tooltipWidth = tooltipEl ? tooltipEl.offsetWidth : 280
      let tooltipHeight = tooltipEl ? tooltipEl.offsetHeight : 160

      // 基础偏移（鼠标右下方）
      let left = mouseX + 15
      let top = mouseY + 20

      // 右边界溢出 -> 放到鼠标左侧
      if (left + tooltipWidth > rect.width) {
        left = mouseX - tooltipWidth - 15
      }
      // 左边界溢出 -> 强制靠左
      left = Math.max(5, left)
      // 下边界溢出 -> 放到鼠标上方
      if (top + tooltipHeight > rect.height) {
        top = mouseY - tooltipHeight - 20
      }
      // 上边界溢出 -> 强制靠上
      top = Math.max(5, top)

      // 最终边界钳制（确保完全在父容器内）
      left = Math.min(left, rect.width - tooltipWidth - 2)
      top = Math.min(top, rect.height - tooltipHeight - 2)

      tooltipX.value = left
      tooltipY.value = top
    } finally {
      rafId = null
    }
  })
}

const handleMouseEnter = (item, event) => {
  // 清除待执行的隐藏定时器
  if (leaveTimer) {
    clearTimeout(leaveTimer)
    leaveTimer = null
  }
  if (!item) return
  showTooltip.value = true
  tooltipContent.value = { ...item }
  // 先渲染提示框，再校准位置
  nextTick(() => {
    if (showTooltip.value) {
      updatePosition(event)
    }
  })
}

const handleMouseMove = (event) => {
  if (showTooltip.value) {
    updatePosition(event)
  }
}

const handleMouseLeave = () => {
  leaveTimer = setTimeout(() => {
    showTooltip.value = false
    tooltipContent.value = { title: '', content: '' }
  }, 100)
}

// 组件卸载时清理定时器和动画
onUnmounted(() => {
  if (leaveTimer) clearTimeout(leaveTimer)
  if (rafId) cancelAnimationFrame(rafId)
})
</script>

<template>
  <div class="right" ref="rightRef">
    <!-- 九个功能热区，增加 aria-describedby 指向提示框 -->
    <div
      class="hotzone save"
      @mouseenter="handleMouseEnter(introductions[0], $event)"
      @mousemove="handleMouseMove"
      @mouseleave="handleMouseLeave"
      aria-label="项目管理按钮组"
      aria-describedby="global-tooltip"
    ></div>
    <div
      class="hotzone circle"
      @mouseenter="handleMouseEnter(introductions[1], $event)"
      @mousemove="handleMouseMove"
      @mouseleave="handleMouseLeave"
      aria-label="编辑按钮组"
      aria-describedby="global-tooltip"
    ></div>
    <div
      class="hotzone realise"
      @mouseenter="handleMouseEnter(introductions[2], $event)"
      @mousemove="handleMouseMove"
      @mouseleave="handleMouseLeave"
      aria-label="验证按钮组"
      aria-describedby="global-tooltip"
    ></div>
    <div
      class="hotzone add"
      @mouseenter="handleMouseEnter(introductions[3], $event)"
      @mousemove="handleMouseMove"
      @mouseleave="handleMouseLeave"
      aria-label="新建模块"
      aria-describedby="global-tooltip"
    ></div>
    <div
      class="hotzone canvas"
      @mouseenter="handleMouseEnter(introductions[4], $event)"
      @mousemove="handleMouseMove"
      @mouseleave="handleMouseLeave"
      aria-label="画布"
      aria-describedby="global-tooltip"
    ></div>
    <div
      class="hotzone gate"
      @mouseenter="handleMouseEnter(introductions[5], $event)"
      @mousemove="handleMouseMove"
      @mouseleave="handleMouseLeave"
      aria-label="画布元件"
      aria-describedby="global-tooltip"
    ></div>
    <div
      class="hotzone verilog"
      @mouseenter="handleMouseEnter(introductions[6], $event)"
      @mousemove="handleMouseMove"
      @mouseleave="handleMouseLeave"
      aria-label="Verilog编辑器"
      aria-describedby="global-tooltip"
    ></div>
    <div
      class="hotzone terminal"
      @mouseenter="handleMouseEnter(introductions[7], $event)"
      @mousemove="handleMouseMove"
      @mouseleave="handleMouseLeave"
      aria-label="输出面板"
      aria-describedby="global-tooltip"
    ></div>
    <div
      class="hotzone attribute"
      @mouseenter="handleMouseEnter(introductions[8], $event)"
      @mousemove="handleMouseMove"
      @mouseleave="handleMouseLeave"
      aria-label="右侧侧边栏"
      aria-describedby="global-tooltip"
    ></div>

    <!-- 使用 Transition 组件实现平滑过渡 -->
    <Transition name="tooltip-fade">
      <div
        v-if="showTooltip"
        ref="tooltipRef"
        id="global-tooltip"
        class="tooltip"
        :style="{ left: `${tooltipX}px`, top: `${tooltipY}px` }"
        role="tooltip"
      >
        <div class="tooltip-title">
          {{ tooltipContent.title }}
        </div>
        <div class="tooltip-content">
          {{ tooltipContent.content }}
        </div>
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.right {
  position: absolute;
  right: 0;
  top: 5%;
  width: 86%;
  height: 95%;
  background: url(../../assets/images/Panel/canvaspannel.png) no-repeat;
  background-size: 100% 100%;
  overflow: visible;
  z-index: 100;
}

/* 热区统一样式 */
.hotzone {
  position: absolute;
  cursor: pointer; /* 去掉问号，改为手型指针 */
  background-color: rgba(59, 130, 246, 0.05);
  border-radius: 2px;
}

/* 各个热区位置/尺寸 */
.save {
  width: 60px;
  height: 24px;
}
.circle {
  left: 62px;
  width: 23px;
  height: 24px;
}
.realise {
  left: 88px;
  width: 36px;
  height: 24px;
}
.add {
  top: 25px;
  right: 110px;
  width: 16px;
  height: 16px;
}
.canvas {
  top: 38px;
  width: 87%;
  height: 49%;
}
.gate {
  top: 140px;
  left: 175px;
  width: 48px;
  height: 50px;
  /* border: red 1px solid; */
}
.verilog {
  bottom: 22%;
  width: 87%;
  height: 22%;
}
.terminal {
  bottom: 0;
  width: 100%;
  height: 20%;
}
.attribute {
  right: 0;
  top: 26px;
  width: 11%;
  height: 75%;
}

/* 提示框样式 */
.tooltip {
  position: absolute;
  display: flex;
  flex-direction: column;
  background-color: rgba(230, 242, 255, 0.98);
  color: #1e2a3a;
  border-radius: 8px;
  border: 1px solid #b8d9ff;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
  padding: 12px 14px;
  width: 300px;
  height: 180px;
  pointer-events: none;
  z-index: 1000;
  backdrop-filter: blur(8px);
  font-family:
    system-ui,
    -apple-system,
    'Segoe UI',
    Roboto,
    sans-serif;
  line-height: 1.5;
  box-sizing: border-box;
  overflow: hidden;
}

/* 过渡动画 */
.tooltip-fade-enter-active,
.tooltip-fade-leave-active {
  transition:
    opacity 0.15s ease,
    transform 0.15s ease;
}
.tooltip-fade-enter-from,
.tooltip-fade-leave-to {
  opacity: 0;
  transform: translateY(5px);
}

/* 标题样式 */
.tooltip-title {
  flex-shrink: 0;
  font-weight: 700;
  font-size: 15px;
  color: #0f3b5c;
  margin-bottom: 10px;
  border-left: 3px solid #3b82f6;
  padding-left: 9px;
  letter-spacing: 0.4px;
  white-space: normal;
  word-break: break-word;
  border-bottom: 1px solid rgba(184, 217, 255, 0.5);
  padding-bottom: 6px;
}

/* 内容区域样式 */
.tooltip-content {
  flex: 1;
  overflow-y: auto;
  font-weight: 400;
  font-size: 13px;
  color: #2c3e50;
  line-height: 1.5;
  text-align: left;
  word-break: break-word;
  padding-right: 6px;
  min-height: 0;
  padding-top: 4px;
}

/* 滚动条美化 */
.tooltip-content::-webkit-scrollbar {
  width: 6px;
}
.tooltip-content::-webkit-scrollbar-track {
  background: #e2e8f0;
  border-radius: 3px;
}
.tooltip-content::-webkit-scrollbar-thumb {
  background: #94a3b8;
  border-radius: 3px;
  transition: background 0.2s ease;
}
.tooltip-content::-webkit-scrollbar-thumb:hover {
  background: #64748b;
}
.tooltip-content {
  scrollbar-width: thin;
  scrollbar-color: #94a3b8 #e2e8f0;
}
</style>
