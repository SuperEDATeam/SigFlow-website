<script></script>

<template>
  <div class="sigflow">
    <div class="left">
      <div class="content">
        <video src="../assets/videos/AI演示.mp4" controls=""></video>
      </div>
    </div>
    <div class="right">
      <h2>AI 自顶向下辅助设计</h2>
      <div class="text">
        预定义“黑箱元件”，支持模块化调用。实现AI顶层设计/底层门电路实现/全流程设计三重开发模式。黑箱元件将设计任务自然拆分为互不干涉的子任务，实现AI并行开发模式
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
  position: relative;
  margin: 0 auto;
  margin-top: 35px;
  padding: 0;
  width: 1200px;
  height: 700px;
  border-radius: 5px;
  background-color: rgba(230, 243, 255, 0.7);
  border: 1px rgb(214, 234, 252) solid;
}

.sigflow .left {
  z-index: 2;
  position: absolute;
  left: 20px;
  width: 780px;
  height: 660px;
  border-radius: 5px;
  margin-top: 20px;
  background: url(../assets/images/background3.png);
  background-size: cover;
}

.sigflow .right {
  z-index: 2;
  position: absolute;
  right: 0;
  width: 380px;
  height: 660px;
  border: 1px black solid;
  margin-top: 20px;
  text-align: center;
}

.sigflow .right h2 {
  margin: 0 auto;
  margin-top: 100px;
}

.sigflow .right .text {
  margin: 0 auto;
  margin-top: 150px;
  padding: 0 20px;
  width: 380px;
  height: 300px;
  font-size: 25px;
}

.sigflow .left .content {
  z-index: 2;
  position: absolute;
  top: 40px;
  right: 20px;
  width: 740px;
  height: 580px;
  border-radius: 10px;
  background-color: rgb(230, 243, 255);
  border: rgb(176, 187, 197);
  box-shadow: 1px 1px 5px rgb(128, 133, 137);
}

.sigflow .left .content video {
  position: absolute;
  right: 0;
  top: 0;
  width: 740px;
  height: 580px;
}
</style>
