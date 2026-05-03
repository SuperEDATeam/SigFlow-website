<script></script>

<template>
  <div class="sigflow">
    <div class="text">每天都受到构建世界级软件的团队信赖</div>
    <ul class="team">
      <li><img src="../assets/images/team1.png" width="100px" height="100px" /></li>
      <li><img src="../assets/images/team2.png" width="100px" height="100px" /></li>
      <li><img src="../assets/images/team1.png" width="100px" height="100px" /></li>
      <li><img src="../assets/images/team2.png" width="100px" height="100px" /></li>
      <li><img src="../assets/images/team3.png" width="100px" height="100px" class="yitong" /></li>
      <li><img src="../assets/images/team4.png" width="100px" height="100px" class="yitong" /></li>
      <li><img src="../assets/images/team1.png" width="100px" height="100px" /></li>
      <li><img src="../assets/images/team2.png" width="100px" height="100px" /></li>
    </ul>
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
  margin: 0 auto;
  margin-top: 50px;
  padding: 0;
  width: 1200px;
  height: 180px;
}

.sigflow .text {
  z-index: 2;
  width: 400px;
  height: 25px;
  text-align: center;
  line-height: 25px;
  margin: 5px auto;
  color: white;
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 12.5px;
}

.sigflow .team {
  z-index: 2;
  width: 1200px;
  height: 120px;
  margin: 0px auto;
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
}

.sigflow .team li {
  z-index: 2;
  width: 140px;
  height: 110px;
  padding: 5px;
  list-style: none;
  text-align: center;
  background-color: rgba(230, 243, 255, 0.5);
  border: 1px rgb(214, 234, 252) solid;
}

.sigflow .team li img {
  z-index: 2;
  border-radius: 50%;
  object-fit: cover;
}

.sigflow .team .yitong {
  z-index: 2;
  border-radius: 0;
}
</style>
