<script></script>

<template>
  <div class="sigflow">
    <div class="left">
      <h2>实时仿真</h2>
      <div class="text">
        通过在画布上放置输入输出元件，如输入输出引脚，时钟元件，接地，VCC等进行实时激励，随后信号计算并显示在画布上
      </div>
    </div>
    <div class="right">
      <div class="content">
        <video src="../assets/videos/实时仿真.mp4" controls></video>
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
  left: 0;
  width: 380px;
  height: 660px;
  border: 1px black solid;
  margin-top: 20px;
  text-align: center;
}

.sigflow .left h2 {
  margin: 0 auto;
  margin-top: 100px;
}

.sigflow .left .text {
  margin: 0 auto;
  margin-top: 150px;
  padding: 0 20px;
  width: 380px;
  height: 300px;
  font-size: 25px;
}

.sigflow .right {
  z-index: 2;
  position: absolute;
  right: 20px;
  width: 780px;
  height: 660px;
  border-radius: 5px;
  margin-top: 20px;
  background: url(../assets/images/background2.png) no-repeat;
  background-size: cover;
}

.sigflow .right .content {
  z-index: 2;
  position: absolute;
  top: 40px;
  left: 20px;
  width: 740px;
  height: 580px;
  border-radius: 10px;
  background-color: rgb(240, 248, 255);
  border: rgb(201, 213, 223);
  box-shadow: 1px 1px 5px rgb(128, 133, 137);
}

.sigflow .right .content video {
  position: absolute;
  right: 0;
  top: 0;
  width: 740px;
  height: 580px;
}
</style>
