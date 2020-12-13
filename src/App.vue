<template>
  <div id="app">
    <div class="header">
      <portal-target name="header-right" class="back" />
      <span class="route-name">
        <div class="icon">
          <font-awesome-icon icon="ship" />
        </div>
      </span>
      <button class="search"><font-awesome-icon icon="search" /></button>
    </div>
    <router-view />
    <!--     <div id="nav">
      <router-link class="nav-link" to="/"
        ><font-awesome-icon icon="home"
      /></router-link>
      |
      <router-link class="nav-link" to="/about">About</router-link>
    </div> -->
  </div>
</template>

<script>
export default {
  name: "App",
  computed: {
    routeName() {
      return this.$route.name;
    },
  },
};
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fefefe;
  background: #3a4255;
  height: 100vh;
}
body {
  margin: 0;
}
.header {
  display: flex;
  justify-content: space-between;
  padding: 20px 12px;
  .back,
  .search {
    height: 44px;
    background: transparent;
    border: none;
    color: white;
    font-size: 22px;
    width: 44px;
    outline: none;
  }
  .route-name {
    font-size: 22px;
    .icon {
      background: transparent;
      width: 40px;
      height: 40px;
      border: 2px solid white;
      border-radius: 40px;
      line-height: 40px;
      font-size: 16px;
    }
  }
}
#nav {
  width: 100vw;
  position: fixed;
  bottom: 0;
  height: 60px;
  background: #3a4255;
  left: 0;
  border-top: 2px solid white;
  display: flex;
  justify-content: space-between;
  .nav-link {
    height: calc(60px - 16px);
    margin: 8px;
    font-size: 22px;
    color: #ebebeb;
  }
}
</style>
