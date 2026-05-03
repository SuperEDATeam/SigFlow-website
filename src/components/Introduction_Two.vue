<script></script>

<template>
  <div class="sigflow">
    <div class="left">
      <div class="content">
        <video src="../assets/videos/离线仿真.mp4" controls=""></video>
      </div>
    </div>
    <div class="right">
      <h2>离线仿真</h2>
      <div class="text">
        不但支持传统电路仿真波形图预览，还实现了离线仿真重演。离线仿真以Verilog代码编写的Testbench为激励，以Debugger模式清晰展现波形图在任意时刻电路的信号状态。直观辅助用户进行验证、调试
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
  background-color: rgb(99, 105, 111);
  border: 1px rgb(78, 83, 88) solid;
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
