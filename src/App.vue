<template>
  <div id="app">
    <div id="nav">
      <!-- <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> -->
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">

html{
  height: 100%;
}

body {
  background-image: url('~@/assets/amster.jpg');
  background-size: cover;
  height: 100%;
  * {
    font-family: "Open Sans", 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
}
</style>
