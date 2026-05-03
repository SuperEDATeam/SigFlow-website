<script setup>
import Topbar from './Project/TopBar.vue'
import LeftBar from './Project/LeftBar.vue'
import RightPannel from './Project/RightPannel.vue'
</script>

<template>
  <div class="sigflow">
    <div class="text">项目架构总览</div>
    <div class="note_book">
      <Topbar></Topbar>
      <LeftBar></LeftBar>
      <RightPannel></RightPannel>
    </div>
  </div>
</template>

<style scoped>
.sigflow {
  z-index: 2;
  position: relative;
  margin: 0 auto;
  padding: 0;
  width: 1200px;
  height: 900px;
  border-radius: 10px;
  /* background: url(../assets/images/background.png) no-repeat; */
  /* background-size: cover; */
  background-color: rgba(255, 255, 255, 0.8);
}

.sigflow .text {
  position: absolute;
  top: 30px;
  width: 100%;
  text-align: center;
  font-size: 40px;
}

.sigflow .note_book {
  z-index: 2;
  position: absolute;
  top: 12%;
  right: 50%;
  transform: translateX(50%);
  width: 1100px;
  height: 750px;
  background-color: rgb(230, 243, 255);
  /* border-radius: 20px; */
  border: 1px rgb(230, 243, 255) solid;
  box-shadow: 1px 1px 10px gray;
}
</style>
