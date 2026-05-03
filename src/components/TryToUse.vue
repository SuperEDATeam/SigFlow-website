<script>
import '../assets/iconfont/iconfont.css'
</script>

<template>
  <div class="sigflow">
    <div class="text">立即试用SigFlow。</div>
    <div class="btns">
      <button>下载Windows版本<i class="iconfont icon-xiazai"></i></button>
      <button>下载MOS版本<i class="iconfont icon-xiazai"></i></button>
      <button>下载Linuix版本<i class="iconfont icon-xiazai"></i></button>
    </div>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  list-style: none;
}

.sigflow {
  z-index: 2;
  margin: 0 auto;
  margin-top: 35px;
  padding: 0;
  width: 1200px;
  height: 250px;
}

.sigflow .text {
  z-index: 2;
  margin: 10px auto;
  width: 1000px;
  height: 150px;
  font-size: 80px;
  text-align: center;
  line-height: 150px;
  color: white;
  background-color: rgba(0, 0, 0, 0.7);
}

.sigflow .btns {
  z-index: 2;
  margin: 10px auto;
  width: 1000px;
  height: 100px;
  /* 新增：使用 Flexbox 实现均匀分布 */
  display: flex;
  justify-content: space-evenly; /* 按钮及两侧间距完全相等 */
  align-items: center; /* 垂直居中 */
}

.sigflow .btns button {
  z-index: 2;
  width: 200px;
  height: 50px;
  border-radius: 25px;
  margin: 0; /* 清除原有 margin，由 flex 控制间距 */
  color: white;
  background-color: black;
  font-size: 17px;
  border: 0.5px black solid;
}

.sigflow .btns button:hover {
  background-color: rgba(51, 49, 49, 0.9);
}
.iconfont {
  font-size: 20px; /* 默认字体大小，单位可以是 px、rem、em 等 */
}
</style>
