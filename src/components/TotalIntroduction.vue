<script>
import '../assets/iconfont/iconfont.css'
</script>

<template>
  <div class="sigflow">
    <div class="introduction">
      SigFlow基于自研结构树，实现代码与电路图实时同步，释放交互潜能，构建插件化生态，重构开源EDA。
    </div>
    <button>下载Windows版本<i class="iconfont icon-xiazai"></i></button>
    <button>下载MOS版本<i class="iconfont icon-xiazai"></i></button>
    <button>下载Linuix版本<i class="iconfont icon-xiazai"></i></button>
  </div>
</template>

<style scoped>
.sigflow {
  z-index: 2;
  margin: 0 auto;
  padding: 0;
  width: 1200px;
  height: 250px;
}

.sigflow .introduction {
  color: white;
  z-index: 2;
  margin-top: 50px;
  width: 600px;
  height: 150px;
  font-size: 30px;
}

.sigflow button {
  z-index: 2;
  width: 200px;
  height: 50px;
  border-radius: 25px;
  margin: 10px;
  margin-left: 0;
  color: white;
  background-color: black;
  font-size: 17px;
  border: 0.5px black solid;
}

.sigflow button:hover {
  background-color: rgba(51, 49, 49, 0.9);
}

.iconfont {
  font-size: 20px; /* 默认字体大小，单位可以是 px、rem、em 等 */
}
</style>
