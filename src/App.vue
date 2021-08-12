<template>
  <h1>{{ title }}</h1>
  <router-view></router-view>
</template>
<script>
import { ref } from "vue";

export default {
  name: "App",
  setup() {
    const title = ref("Bienvenidos al curso de Vue.js version 3");

    return {
      title,
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.margin-15 {
  margin-bottom: 15px;
}
</style>
