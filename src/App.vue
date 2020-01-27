<template>
  <div id="app">
    <img class="nba" src="../public/img/icons/nba-seeklogo.com.svg" alt="" />
    <router-view />
  </div>
</template>

<style lang="scss">
body,
html {
  margin: 0;
  padding: 0;
  background: rgb(238, 246, 255);
}
img.nba {
  margin: 2rem;
  width: 200px;
}
.banner {
  padding: 4rem 0;
  color: #fff;
  background: linear-gradient(
    139deg,
    rgba(12, 2, 103, 1) 0%,
    rgba(0, 236, 255, 1) 100%
  );
}
#app {
  font-family: "Open Sans", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  letter-spacing: -0.5px;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}
</style>
