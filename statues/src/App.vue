<template>

  <button @click="togglePaintings">{{ pbtnText }}</button>
  <div v-if="this.showPaintings">
    <h1>Paintings</h1>
    <Paintings />
  </div>

  <br>

  <button @click="toggleStatues">{{ sbtnText }}</button>
  <div v-if="this.showStatues">
    <h1>Statues</h1>
    <Statues />
  </div>
  
</template>

<script>
import Paintings from './components/Paintings.vue';
import Statues from "./components/Statues.vue";

export default {
  components: { Paintings ,Statues },
  name: "App",
  data() {
    return {
      showPaintings: false,
      showStatues: false,
      pbtnText: "Show paintings",
      sbtnText: "Show statues"
    }
  },
  methods: {
    togglePaintings() {
      this.showPaintings = !this.showPaintings

      if(this.pbtnText == "Show paintings") {
        this.pbtnText = "Hide paintings"
      } else {
        this.pbtnText = "Show paintings"
      }
    },
    toggleStatues() {
      this.showStatues = !this.showStatues

      if(this.sbtnText == "Show statues") {
        this.sbtnText = "Hide statues"
      } else {
        this.sbtnText = "Show statues"
      }
    }
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
