<template>
  <div id="app">
    <nav>
      <router-link to="/">上手</router-link> |
      <router-link to="/event">移动事件并调整大小</router-link> |
      <router-link to="/grid">多个栅格</router-link> |
      <router-link to="/drag">拖动允许/忽略元素</router-link> |
      <router-link to="/mirrored">镜像反转栅格布局</router-link> |
      <router-link to="/responsive">响应式</router-link> |
      <router-link to="/collision">防止碰撞</router-link> |
      <router-link to="/set">响应预定义的布局</router-link> |
      <router-link to="/add">动态添加/删除</router-link> |
      <router-link to="/dragin">从外面拖动</router-link> |
      <router-link to="/draglink">拖动栅格元素绑定到容器</router-link> |
    </nav>
    <router-view/>
  </div>
</template>

<style>
/* *{
  margin:0;
  padding:0;
  border:0;
} */
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
