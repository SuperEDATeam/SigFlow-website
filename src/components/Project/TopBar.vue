<template>
  <div class="topbar">
    <div class="img"></div>
  </div>
</template>

<style scoped>
.topbar {
  position: absolute;
  width: 100%;
  height: 5%; /* 根据图片高度或设计需求设置 */
  z-index: 3;
}

.topbar .img {
  position: absolute;
  top: 0;
  right: 0;
  width: 100%;
  height: 100%;
  background: url('../../assets/images/Panel/headbar.png') no-repeat;
  background-size: 100% 100%; /* 或 contain，根据需要调整 */
  background-position: center;
}
</style>
