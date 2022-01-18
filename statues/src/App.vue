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
          <button @click="deleteStatue(s.id)">Delete</button>
          <button @click="editStatue(s)">Edit</button>
        </td>
      </tr>
      <tr>
        <td>
          <input type="text" name="person" v-model="temp.person" />
        </td>
        <td>
          <input type="number" name="height" v-model="temp.height" />
        </td>
        <td>
          <input type="number" name="price" v-model="temp.price" />
        </td>
        <td>
          <input type="button" @click="newStatue" value="Add" v-if="!this.saving"/>
          <button @click="saveStatue" v-if="this.saving">Save</button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
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
  methods: {
    async getStatues() {
      const response = await fetch("http://127.0.0.1:8000/api/statues");
      const data = await response.json();
      this.statues = data;
    },
    async editStatue(selected) {
      this.temp.id = selected.id
      this.temp.person = selected.person
      this.temp.height = selected.height
      this.temp.price = selected.price

      this.saving = true

      console.log("saving:" + this.saving)
    },      
    async saveStatue() {
      const response = await fetch(`http://127.0.0.1:8000/api/statues/${this.temp.id}`, {
          method: 'PATCH',
          headers: {
            "Content-Type": "application/json",
            "Accept": "application/json"
          }, 
          body: JSON.stringify(this.temp)
        })

      console.log(response)

      await this.getStatues()

    this.resetTemp()

      this.saving = false
      console.log("saving:" + this.saving)
    },
    async deleteStatue(selectedId) {
      const response = await fetch(`http://127.0.0.1:8000/api/statues/${selectedId}`, {
        method: 'DELETE'
      })

      await this.getStatues()
      console.log(response)
    },
    async newStatue() {
      const response = await fetch("http://127.0.0.1:8000/api/statues", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Accept": "application/json"
        }, 
        body: JSON.stringify(this.temp)
        })
      
      console.log(response)
      await this.getStatues()
      this.resetTemp()
    },
    resetTemp() {
        this.temp.id = 0
        this.temp.person = ""
        this.temp.height = ""
        this.temp.price = ""
    }
  },
  mounted() {
    this.getStatues();
  },
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
