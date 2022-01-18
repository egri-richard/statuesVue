<template>
  <h1>Paintings</h1>
  <Paintings />
  <br>

  <h1>Statues</h1>
  <Statues />
</template>

<script>
import Paintings from './components/Paintings.vue';
import Statues from "./components/Statues.vue";

export default {
  components: { Paintings ,Statues },
  name: "App",
  data() {
    return {}
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
