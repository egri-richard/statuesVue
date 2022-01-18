<template>
  <Statues />
</template>

<script>
import Statues from "./components/Statues.vue";

export default {
  components: { Statues },
  name: "App",
  data() {
    return {
      saving: false,
      statues: Array,
      temp: {
        id: 0,
        person: "",
        height: "",
        price: "",
      },
    };
  },
  methods: {},
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
