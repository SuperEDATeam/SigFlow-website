<script></script>

<template>
  <div class="sigflow">
    <div class="text">SuperEDA是一支专注于构建软件开发未来的应用研究团队。</div>
    <div class="joinus">加入我们 —></div>
    <img src="../assets/images/SuperEDA.png" />
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
  position: relative;
  margin: 0 auto;
  margin-top: 35px;
  padding: 0;
  width: 1200px;
  height: 410px;
  background-color: rgba(230, 243, 255, 0.7);
  border: 1px rgb(214, 234, 252) solid;
}

.sigflow .text {
  z-index: 2;
  position: absolute;
  left: 20px;
  top: 140px;
  width: 380px;
  height: 70px;
  font-size: 25px;
}

.sigflow .joinus {
  z-index: 2;
  position: absolute;
  top: 240px;
  left: 20px;
  width: 380px;
  height: 30px;
  line-height: 30px;
  color: skyblue;
}

.sigflow .joinus:hover {
  cursor: pointer;
  color: rgb(114, 147, 160);
}

.sigflow img {
  z-index: 2;
  position: absolute;
  top: 10px;
  right: 10px;
  width: 780px;
  height: 390px;
}
</style>
