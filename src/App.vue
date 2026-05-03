<script setup>
import HeadBar from './components/HeadBar.vue'
import TotalIntroduction from './components/TotalIntroduction.vue'
import UserandName from './components/UserandName.vue'
import ProjectDemo from './components/ProjectDemo.vue'
import TrustTeam from './components/TrustTeam.vue'
import Introduction_One from './components/Introduction_One.vue'
import Introduction_Two from './components/Introduction_Two.vue'
import Introduction_Three from './components/Introduction_Three.vue'
import Introduction_Four from './components/Introduction_Four.vue'
import Introduction_Five from './components/Introduction_Five.vue'
import TeamComments from './components/TeamComments.vue'
import CoreCompetition from './components/CoreCompetition.vue'
import JoinUs from './components/JoinUs.vue'
import TrytoUse from './components/TryToUse.vue'
import BottomBar from './components/BottomBar.vue'
</script>

<template>
  <div class="app">
    <!-- 新增根容器 -->
    <div class="total_content">
      <!-- 将除 BottomBar 外的所有组件包裹起来 -->
      <HeadBar />
      <TotalIntroduction />
      <UserandName></UserandName>
      <ProjectDemo />
      <TrustTeam />
      <Introduction_One />
      <Introduction_Two />
      <Introduction_Three />
      <Introduction_Four />
      <Introduction_Five />
      <CoreCompetition></CoreCompetition>
      <TeamComments />

      <JoinUs />
      <TrytoUse />
    </div>
    <BottomBar />
  </div>
</template>

<style>
html,
body {
  margin: 0;
  padding: 0;
  height: 100%;
}

body {
  /* 背景图片（使用正确的别名路径） */
  background-image: url('./assets/images/bgi.jpg');
  background-repeat: no-repeat;
  background-attachment: fixed; /* 背景固定，滚动时不移动 */
  background-size: cover;
  background-position: center;
}

.app {
  margin: 0;
  padding: 0;
  min-height: 100vh; /* 最小高度铺满视口 */
  display: flex;
  flex-direction: column; /* 垂直排列 total_content 和 BottomBar */
}

.total_content {
  flex: 1; /* 占据剩余空间，使 BottomBar 自然推到底部（如果内容不足） */
  background-color: rgba(240, 248, 255, 0.1); /* 半透白，让背景图透出，同时保证文字可读 */
  /* 移除了固定高度 height: 8030px，让内容撑开 */
}
</style>
