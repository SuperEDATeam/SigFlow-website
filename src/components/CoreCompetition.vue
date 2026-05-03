<script setup>
import { ref, onMounted } from 'vue'
import * as echarts from 'echarts'

// 竞品数据 - 根据图片内容更新
const competitors = ref([
  {
    name: 'Xilinx Vivado',
    functionBoundary: '工业级FPGA全流程开发',
    interaction: '代码为主+图形辅助',
    hdl: '✓',
    domestic: '否',
    openSource: '商业',
    sync: '×',
    link: 'https://www.amd.com/en/products/software/adaptive-socs-and-fpgas/vivado.html',
    linkText: '官网',
  },
  {
    name: 'Intel Quartus Prime',
    functionBoundary: 'SoC系统集成/IP连接',
    interaction: '图形化模块连接+参数配置',
    hdl: '✓',
    domestic: '否',
    openSource: '商业',
    sync: '×',
    link: 'https://www.intel.com/content/www/us/en/products/details/fpga/development-tools/quartus-prime.html',
    linkText: '官网',
  },
  {
    name: 'Vivado IP Integrator',
    functionBoundary: 'IP级系统集成',
    interaction: '图形化连接（Block Diagram）',
    hdl: '✓',
    domestic: '否',
    openSource: '商业',
    sync: '×',
    link: 'https://www.amd.com/en/products/software/adaptive-socs-and-fpgas/vivado.html',
    linkText: 'AMD官网',
  },
  {
    name: 'Synopsys Verdi',
    functionBoundary: '芯片级调试与验证',
    interaction: '代码+波形+层次视图',
    hdl: '✓',
    domestic: '否',
    openSource: '商业',
    sync: '×',
    link: 'https://www.synopsys.com/verification/debug/verdi.html',
    linkText: '官网',
  },
  {
    name: 'Cadence Virtuoso',
    functionBoundary: '模拟/混合信号IC设计',
    interaction: '原理图+版图+仿真',
    hdl: '✓',
    domestic: '否',
    openSource: '商业',
    sync: '×',
    link: 'https://www.cadence.com/en_US/home/tools/custom-ic-analog-rf-design/virtuoso-platform.html',
    linkText: '官网',
  },
  {
    name: 'Logisim',
    functionBoundary: '教学级逻辑电路仿真',
    interaction: '纯图形（门级拖拽）',
    hdl: '×',
    domestic: '否',
    openSource: '开源',
    sync: '×',
    link: 'https://www.cburch.com/logisim/',
    linkText: '官网',
  },
  {
    name: 'Logisim Evolution',
    functionBoundary: '扩展版逻辑仿真',
    interaction: '图形化+简单工程管理',
    hdl: '×',
    domestic: '否',
    openSource: '开源',
    sync: '×',
    link: 'https://github.com/logisim-evolution/logisim-evolution',
    linkText: 'GitHub',
  },
  {
    name: 'Digital',
    functionBoundary: '高性能逻辑仿真（偏教学）',
    interaction: '图形化（模块化）',
    hdl: '×',
    domestic: '否',
    openSource: '开源',
    sync: '×',
    link: 'https://github.com/hneemann/Digital',
    linkText: 'GitHub',
  },
  {
    name: 'CircuitVerse',
    functionBoundary: 'Web逻辑仿真+社区分享',
    interaction: 'Web GUI（拖拽）',
    hdl: '×',
    domestic: '否',
    openSource: '开源',
    sync: '×',
    link: 'https://circuitverse.org/',
    linkText: '官网',
  },
  {
    name: 'SigFlow',
    functionBoundary: 'Verilog全流程前端',
    interaction: '代码+图形双向同步',
    hdl: '✓',
    domestic: '是',
    openSource: '开源',
    sync: '✓',
    link: '#',
    linkText: '了解更多',
    isHighlight: true,
  },
])

// 图表数据：功能丰富度评分（1-10）
const getScore = (name) => {
  const scores = {
    'Xilinx Vivado': 9,
    'Intel Quartus Prime': 9,
    'Vivado IP Integrator': 8,
    'Synopsys Verdi': 9,
    'Cadence Virtuoso': 9,
    Logisim: 5,
    'Logisim Evolution': 6,
    Digital: 6,
    CircuitVerse: 6,
    SigFlow: 10,
  }
  return scores[name] || 5
}

// 图表数据：发布年份（模拟）
const getYear = (name) => {
  const years = {
    'Xilinx Vivado': 2012,
    'Intel Quartus Prime': 2011,
    'Vivado IP Integrator': 2013,
    'Synopsys Verdi': 1996,
    'Cadence Virtuoso': 1991,
    Logisim: 2001,
    'Logisim Evolution': 2015,
    Digital: 2016,
    CircuitVerse: 2018,
    SigFlow: 2024,
  }
  return years[name] || 2010
}

const barChartRef = ref(null)
const lineChartRef = ref(null)

onMounted(() => {
  // 直方图：功能丰富度评分 - 蓝色主题
  const barChart = echarts.init(barChartRef.value)
  barChart.setOption({
    tooltip: { trigger: 'axis', axisPointer: { type: 'shadow' } },
    grid: { left: '12%', right: '5%', top: '15%', bottom: '10%', containLabel: true },
    xAxis: {
      type: 'category',
      data: competitors.value.map((c) => c.name),
      axisLabel: { rotate: 30, color: '#1e3a5f', interval: 0, fontSize: 10 },
      axisLine: { lineStyle: { color: '#3b82f6' } },
    },
    yAxis: {
      type: 'value',
      name: '功能丰富度评分',
      nameTextStyle: { color: '#1e3a5f' },
      axisLabel: { color: '#1e3a5f' },
      splitLine: { lineStyle: { color: '#dbeafe' } },
      max: 11,
    },
    series: [
      {
        name: '评分',
        type: 'bar',
        data: competitors.value.map((c) => getScore(c.name)),
        itemStyle: {
          color: (params) => {
            return params.name === 'SigFlow' ? '#3b82f6' : '#93c5fd'
          },
          borderRadius: [6, 6, 0, 0],
        },
        barWidth: 25,
        label: {
          show: true,
          position: 'top',
          color: '#1e3a5f',
        },
      },
    ],
  })

  // 折线图：发布年份趋势 - 蓝色主题
  const lineChart = echarts.init(lineChartRef.value)
  lineChart.setOption({
    tooltip: { trigger: 'axis' },
    grid: { left: '12%', right: '5%', top: '15%', bottom: '10%', containLabel: true },
    xAxis: {
      type: 'category',
      data: competitors.value.map((c) => c.name),
      axisLabel: { rotate: 30, color: '#1e3a5f', interval: 0, fontSize: 10 },
      axisLine: { lineStyle: { color: '#3b82f6' } },
    },
    yAxis: {
      type: 'value',
      name: '发布年份',
      nameTextStyle: { color: '#1e3a5f' },
      axisLabel: { color: '#1e3a5f' },
      splitLine: { lineStyle: { color: '#dbeafe' } },
    },
    series: [
      {
        name: '首次发布年份',
        type: 'line',
        data: competitors.value.map((c) => getYear(c.name)),
        smooth: true,
        lineStyle: { color: '#2563eb', width: 3 },
        symbol: 'circle',
        symbolSize: 8,
        symbolColor: (params) => {
          return params.name === 'SigFlow' ? '#1d4ed8' : '#3b82f6'
        },
        areaStyle: { color: 'rgba(59, 130, 246, 0.08)' },
        label: { show: true, color: '#1e3a5f', rotate: 0, offset: [0, -12] },
      },
    ],
  })

  window.addEventListener('resize', () => {
    barChart.resize()
    lineChart.resize()
  })
})
</script>

<template>
  <div class="core-competition">
    <h2 class="section-title">核心竞品</h2>
    <p class="section-description">
      EDA开源生态链中的前端空白，同时开创了语言与图形同步交互的标准化设计新范式。
    </p>

    <!-- 图表卡片区域（两列布局） -->
    <div class="charts-row">
      <div class="chart-card">
        <h3>竞品功能丰富度对比</h3>
        <div ref="barChartRef" class="chart-container"></div>
      </div>
      <div class="chart-card">
        <h3>竞品发展年份趋势</h3>
        <div ref="lineChartRef" class="chart-container"></div>
      </div>
    </div>

    <!-- 竞品对比表格 - 蓝色主题，对齐优化 -->
    <div class="table-wrapper">
      <table class="competition-table">
        <thead>
          <tr>
            <th class="col-name">软件名称</th>
            <th class="col-boundary">功能边界</th>
            <th class="col-interaction">交互方式</th>
            <th class="col-hdl">HDL</th>
            <th class="col-domestic">国产</th>
            <th class="col-opensource">开源</th>
            <th class="col-sync">双向同步</th>
            <th class="col-link">链接</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="item in competitors"
            :key="item.name"
            :class="{ 'highlight-row': item.isHighlight }"
          >
            <td class="col-name">
              <strong :class="{ 'highlight-text': item.isHighlight }">{{ item.name }}</strong>
            </td>
            <td class="col-boundary">{{ item.functionBoundary }}</td>
            <td class="col-interaction">{{ item.interaction }}</td>
            <td class="col-hdl center">
              <span :class="item.hdl === '✓' ? 'check-mark' : 'cross-mark'">{{ item.hdl }}</span>
            </td>
            <td class="col-domestic center">
              <span :class="['badge', item.domestic === '是' ? 'badge-yes' : 'badge-no']">
                {{ item.domestic }}
              </span>
            </td>
            <td class="col-opensource center">
              <span
                :class="[
                  'badge',
                  item.openSource === '开源' ? 'badge-opensource' : 'badge-commercial',
                ]"
              >
                {{ item.openSource }}
              </span>
            </td>
            <td class="col-sync center">
              <span v-if="item.sync === '✓'" class="sync-badge">✓</span>
              <span v-else class="sync-badge-no">×</span>
            </td>
            <td class="col-link">
              <a :href="item.link" target="_blank" rel="noopener noreferrer" class="link">{{
                item.linkText
              }}</a>
            </td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- SigFlow 核心亮点说明 - 蓝色主题 -->
    <div class="highlight-box">
      <div class="highlight-icon">🔵</div>
      <div class="highlight-content">
        <strong>SigFlow</strong> 是目前唯一实现
        <span class="emphasize">Verilog 代码与电路图双向实时同步的开源 EDA 前端工具</span>，
        同时也是少数的国产 EDA 开源方案之一。
      </div>
    </div>
  </div>
</template>

<style scoped>
.core-competition {
  font-family:
    system-ui,
    -apple-system,
    'Segoe UI',
    Roboto,
    sans-serif;
  padding: 1.5rem;
  border-radius: 20px;
  max-width: 1400px;
  margin: 2rem auto;
  background: linear-gradient(135deg, #ffffff 0%, #f0f9ff 100%);
}

.section-title {
  font-size: 1.8rem;
  font-weight: 700;
  color: #1e3a5f;
  margin: 0 0 0.5rem 0;
  letter-spacing: -0.02em;
}

.section-description {
  font-size: 1rem;
  color: #475569;
  margin: 0 0 2rem 0;
  line-height: 1.6;
  border-left: 4px solid #3b82f6;
  padding-left: 1rem;
  background: linear-gradient(90deg, rgba(59, 130, 246, 0.05) 0%, transparent 100%);
  border-radius: 0 8px 8px 0;
}

.charts-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
  margin-bottom: 2.5rem;
}

.chart-card {
  background: #ffffff;
  border-radius: 20px;
  border: 1px solid #bfdbfe;
  padding: 1.2rem 1.2rem 0.5rem 1.2rem;
  box-shadow: 0 8px 20px rgba(59, 130, 246, 0.08);
  transition:
    transform 0.2s,
    box-shadow 0.2s;
}

.chart-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 28px rgba(59, 130, 246, 0.12);
}

.chart-card h3 {
  margin: 0 0 1rem 0;
  font-size: 1.1rem;
  font-weight: 600;
  color: #1e40af;
  padding-left: 0.75rem;
  border-left: 3px solid #3b82f6;
}

.chart-container {
  width: 100%;
  height: 280px;
}

/* 表格样式 - 蓝色主题，对齐优化 */
.table-wrapper {
  overflow-x: auto;
  border-radius: 16px;
  border: 1px solid #bfdbfe;
  background: white;
  box-shadow: 0 4px 12px rgba(59, 130, 246, 0.06);
}

.competition-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.85rem;
  min-width: 1100px;
}

.competition-table th {
  background: linear-gradient(135deg, #1e40af 0%, #2563eb 100%);
  color: white;
  font-weight: 600;
  padding: 0.9rem 1rem;
  white-space: nowrap;
  font-size: 0.85rem;
  letter-spacing: 0.3px;
}

/* 列宽控制 */
.col-name {
  width: 10%;
}
.col-boundary {
  width: 22%;
}
.col-interaction {
  width: 18%;
}
.col-hdl {
  width: 6%;
}
.col-domestic {
  width: 6%;
}
.col-opensource {
  width: 8%;
}
.col-sync {
  width: 8%;
}
.col-link {
  width: 8%;
}

.competition-table td {
  padding: 0.85rem 1rem;
  border-bottom: 1px solid #e0e7ff;
  color: #1e293b;
  vertical-align: middle;
  background-color: white;
}

.competition-table tbody tr:hover td {
  background-color: #eff6ff;
}

.highlight-row td {
  background-color: #eef2ff !important;
  border-bottom: 1px solid #c7d2fe;
}

.highlight-text {
  color: #1d4ed8;
  font-weight: 700;
}

.center {
  text-align: center;
}

/* 符号样式 */
.check-mark {
  display: inline-block;
  width: 24px;
  height: 24px;
  line-height: 22px;
  text-align: center;
  background-color: #10b981;
  color: white;
  border-radius: 50%;
  font-weight: bold;
  font-size: 14px;
}

.cross-mark {
  display: inline-block;
  width: 24px;
  height: 24px;
  line-height: 22px;
  text-align: center;
  background-color: #ef4444;
  color: white;
  border-radius: 50%;
  font-weight: bold;
  font-size: 14px;
}

/* 徽章样式 - 蓝色主题 */
.badge {
  display: inline-block;
  padding: 0.2rem 0.7rem;
  border-radius: 30px;
  font-size: 0.75rem;
  font-weight: 500;
  min-width: 44px;
  text-align: center;
}

.badge-yes {
  background-color: #dbeafe;
  color: #1e40af;
  border: 1px solid #93c5fd;
}

.badge-no {
  background-color: #f1f5f9;
  color: #64748b;
  border: 1px solid #cbd5e1;
}

.badge-opensource {
  background-color: #dbeafe;
  color: #1e40af;
  border: 1px solid #93c5fd;
}

.badge-commercial {
  background-color: #f1f5f9;
  color: #64748b;
  border: 1px solid #cbd5e1;
}

/* 双向同步徽章 */
.sync-badge {
  display: inline-block;
  width: 26px;
  height: 26px;
  line-height: 24px;
  text-align: center;
  background-color: #10b981;
  color: white;
  border-radius: 50%;
  font-weight: bold;
  font-size: 14px;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
}

.sync-badge-no {
  display: inline-block;
  width: 26px;
  height: 26px;
  line-height: 24px;
  text-align: center;
  background-color: #e2e8f0;
  color: #94a3b8;
  border-radius: 50%;
  font-weight: bold;
  font-size: 14px;
}

.link {
  color: #2563eb;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.8rem;
  transition: color 0.2s;
}

.link:hover {
  color: #1d4ed8;
  text-decoration: underline;
}

/* 高亮说明框 - 蓝色主题 */
.highlight-box {
  background: linear-gradient(135deg, #eff6ff 0%, #dbeafe 100%);
  border-left: 5px solid #3b82f6;
  border-radius: 12px;
  padding: 1rem 1.5rem;
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-top: 1.5rem;
  box-shadow: 0 2px 8px rgba(59, 130, 246, 0.1);
}

.highlight-icon {
  font-size: 1.6rem;
}

.highlight-content {
  font-size: 0.95rem;
  color: #1e3a5f;
  line-height: 1.5;
}

.emphasize {
  font-weight: 700;
  color: #1d4ed8;
  background-color: rgba(59, 130, 246, 0.12);
  padding: 0.1rem 0.3rem;
  border-radius: 6px;
}
</style>
