<template>
  <div>
    <table>
      <tr>
        <th>Person</th>
        <th>Height</th>
        <th>Price</th>
        <th>Operations</th>
      </tr>
      <tr v-for="s in statues" :key="s.id">
        <td>{{ s.person }}</td>
        <td>{{ s.height }}</td>
        <td>{{ s.price }}</td>
        <td>
          <button>Delete</button>
          <button>Edit</button>
        </td>
      </tr>
      <tr>

      </tr>
    </table>
  </div>
</template>

<script>

export default {
  name: 'App',
  components: {
  },
  data() {
    return { 
      statues: Array
    }
  },
  methods: {
    async getStatues() {
      let response = await fetch("http://127.0.0.1:8000/api/statues")
      let data = await response.json()
      this.statues = data
    }
  },
  mounted() {
    this.getStatues()
  }
}
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
