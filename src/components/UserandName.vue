<script setup>
import { onMounted, ref } from 'vue'
import * as echarts from 'echarts'

// 饼图容器
const pieChartRef = ref(null)

onMounted(() => {
  // 目标用户分布饼图（模拟数据）
  const pieChart = echarts.init(pieChartRef.value)
  pieChart.setOption({
    tooltip: { trigger: 'item' },
    legend: { orient: 'vertical', left: 'left', textStyle: { color: '#2c3e50' } },
    series: [
      {
        name: '目标用户',
        type: 'pie',
        radius: ['45%', '70%'],
        avoidLabelOverlap: false,
        itemStyle: {
          borderRadius: 10,
          borderColor: '#fff',
          borderWidth: 2,
        },
        label: { color: '#2c3e50' },
        data: [
          { value: 42, name: '开源EDA用户' },
          { value: 28, name: '电子专业学生' },
          { value: 18, name: 'FPGA开发者' },
          { value: 12, name: '数字IC架构师' },
        ],
        color: ['#7bb9ff', '#9ec5ff', '#b8d9ff', '#d4eaff'],
      },
    ],
  })

  // 响应式
  window.addEventListener('resize', () => {
    pieChart.resize()
  })
})
</script>

<template>
  <div class="sigflow">
    <div class="user-name-container">
      <div class="product-section">
        <h1 class="product-name">SigFlow</h1>
        <p class="product-meaning">Signal Flow · Workflow</p>
        <p class="product-description">
          既指代逻辑电路中信号的传播结构，也体现以工作流驱动设计流程的理念， 同时隐喻打破 Verilog
          与逻辑电路图之间信息流动壁垒的创新范式。
        </p>
      </div>

      <div class="target-section">
        <h2 class="target-title">目标用户</h2>
        <div class="target-list">
          <span class="target-item">开源EDA生态用户</span>
          <span class="target-item">电子专业学生</span>
          <span class="target-item">FPGA开发者</span>
          <span class="target-item">数字IC架构师</span>
        </div>
        <!-- 饼图容器 -->
        <div ref="pieChartRef" class="chart-container pie-chart"></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.sigflow {
  z-index: 2;
  margin: 35px auto;
  padding: 0;
  width: 1200px;
  min-height: 700px; /* 增加高度以容纳图表 */
  border-radius: 5px;
}

.user-name-container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 2.5rem 3rem;
  border-radius: 28px;
  box-shadow: 0 12px 30px -8px rgba(0, 100, 200, 0.8);
  border: 1px solid #d9ecff;
  font-family:
    system-ui,
    -apple-system,
    sans-serif;
  background-color: rgba(255, 255, 255, 0.7);
}

.product-name {
  margin: 0 0 0.2rem;
  font-size: 3.2rem;
  font-weight: 600;
  color: black;
}

.product-meaning {
  margin: 0 0 1rem;
  font-size: 1.2rem;
  color: rgba(0, 0, 0, 0.5);
  border-bottom: 1px solid #e1f0ff;
  padding-bottom: 1.2rem;
}

.product-description {
  margin: 0 0 2.5rem;
  padding: 2%;
  font-size: 1.1rem;
  line-height: 1.7;
  color: black;
  background-color: rgba(135, 206, 235, 0.5);
  border-radius: 20px;
}

.target-title {
  margin: 1.5rem 0 1.2rem;
  font-size: 1.4rem;
  font-weight: 500;
  color: black;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.target-title::before {
  content: '';
  width: 5px;
  height: 1.5rem;
  background: #7bb9ff;
  border-radius: 4px;
}

.target-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.8rem 1.2rem;
  margin-bottom: 2rem;
}

.target-item {
  background-color: #ebf5ff;
  color: #1e405e;
  padding: 0.6rem 1.6rem;
  border-radius: 40px;
  font-size: 1rem;
  border: 1px solid #c8e2ff;
  transition: 0.15s;
  font-weight: 450;
}

.target-item:hover {
  background-color: #d9ecff;
  border-color: #9ec5ff;
  transform: translateY(-2px);
}

.chart-container {
  width: 100%;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 20px;
  border: 1px solid #e1f0ff;
  padding: 1rem;
  margin: 1.5rem 0;
}

.pie-chart {
  height: 280px;
}
</style>
