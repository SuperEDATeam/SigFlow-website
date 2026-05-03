<script setup>
import { ref } from 'vue'
const videoRef = ref(null)
const playVideo = () => {
  const video = videoRef.value
  video.playbackRate = 6
  video.play()
}

const pauseAndReset = () => {
  const video = videoRef.value
  video.pause()
  video.currentTime = 0
}
</script>

<template>
  <div class="sigflow">
    <div class="box">
      <div class="video_box">
        <video
          ref="videoRef"
          src="../assets/images/active.mp4"
          class="video"
          @mouseenter="playVideo"
          @mouseleave="pauseAndReset"
        ></video>
      </div>
      <div class="name">SigFlow</div>
      <div class="login">登录</div>
      <div class="download">下载</div>
    </div>
  </div>
</template>

<style scoped>
.sigflow {
  /* 移除 fixed 定位，使其成为普通块级元素 */
  width: 100%;
  /* background-color: rgba(240, 248, 255, 0.1); 与页面背景一致的半透白 */
  display: flex;
  align-items: center;
  margin: 0;
  padding: 10px 0;
  justify-content: center;
  /* 如果不需要阴影或边框可忽略，此处不再需要 z-index 和定位属性 */
}

.sigflow .box {
  z-index: 2;
  display: flex;
  align-items: center;
  margin: 0 auto;
  padding: 0;
  width: 1200px;
  height: 100px;
}

.sigflow .video_box .video {
  z-index: 2;
  margin: 0 auto;
  padding-left: 0 auto;
  width: 40px;
  height: 40px;
}

.sigflow .name {
  z-index: 2;
  margin: 0;
  margin-left: 10px;
  padding: 0;
  width: 80px;
  height: 40px;
  line-height: 40px;
  font-family: 'Segoe UI Black';
  font-size: 20px;
  color: white;
}

.sigflow .login {
  z-index: 2;
  margin-left: auto;
  width: 40px;
  height: 40px;
  line-height: 40px;
  color: white;
}

.sigflow .download {
  z-index: 2;
  margin-left: 10px;
  width: 80px;
  height: 40px;
  color: white;
  background-color: black;
  line-height: 40px;
  text-align: center;
  border-radius: 20px;
  border: 0.5px black solid;
}

.sigflow .download:hover {
  background-color: rgba(51, 49, 49, 0.9);
}
</style>
