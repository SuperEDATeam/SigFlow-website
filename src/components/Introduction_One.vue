<script></script>

<template>
  <div class="sigflow">
    <div class="left">
      <h2>Verilog&电路图同步编辑</h2>
      <div class="text">
        在传统IDE与电路设计的基础功能之上，我们采用自研的解析引擎，完成了代码与门级电路图之间的毫秒级双向转化，极大地降低了逻辑构建的认知负荷
      </div>
    </div>
    <div class="right">
      <div class="content">
        <video src="../assets/videos/同步演示.mp4" controls></video>
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
  background-color: rgb(179, 194, 209);
  border: 1px rgb(156, 171, 187) solid;
}

.sigflow .right .content {
  z-index: 2;
  position: absolute;
  top: 40px;
  left: 40px;
  width: 740px;
  height: 580px;
  border-radius: 10px 0 0 10px;
  background-color: rgb(240, 248, 255);
  border: rgb(201, 213, 223);
  box-shadow: -5px 1px 5px rgb(128, 133, 137);
}

.sigflow .right .content video {
  position: absolute;
  right: 0;
  top: 0;
  width: 740px;
  height: 580px;
}
</style>
