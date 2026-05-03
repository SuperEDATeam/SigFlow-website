<script></script>

<template>
  <div class="sigflow">
    <div class="left">
      <h2>插件系统</h2>
      <div class="text">
        基于动态链接库 (DLL)
        的插件架构，我们研发了一套插件介入协议，支持插入Verilator、iVerilog，Yosys等开源工具链下游，以增强软件的仿真、综合性能
      </div>
    </div>
    <div class="right">
      <div class="content">
        <video src="../assets/videos/FPGA插件集成.mp4" controls></video>
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
