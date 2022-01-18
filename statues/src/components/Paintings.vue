<template>
    <table>
    <tr>
      <th>Title</th>
      <th>Year</th>
      <th>On Display</th>
      <th>Operations</th>
    </tr>
    <tr v-for="p in paintings" :key="p.id">
      <td>{{ p.title }}</td>
      <td>{{ p.year }}</td>
      <td>{{ p.on_display }}</td>
      <td>
        <button @click="deletePainting(p.id)">Delete</button>
        <button @click="editPainting(p)">Edit</button>
      </td>
    </tr>
    <tr>
      <td>
        <input type="text" name="person" v-model="temp.title" />
      </td>
      <td>
        <input type="number" name="height" v-model="temp.year" />
      </td>
      <td>
        <input type="checkbox" name="price" v-model="temp.on_display" />
      </td>
      <td>
        <input
          type="button"
          @click="newPainting"
          value="Add"
          v-if="!this.saving"
        />
        <button @click="savePainting" v-if="this.saving">Save</button>
      </td>
    </tr>
  </table>
</template>

<script>
export default {
  name: "Paintings",
  data() {
    return {
      saving: false,
      paintings: Array,
      temp: {
        id: 0,
        title: "",
        year: 0,
        on_display: false,
      },
    }
  },
  methods: {
      async getPaintings() {
      const response = await fetch("http://127.0.0.1:8000/api/paintings");
      const data = await response.json();
      this.paintings = data;
    },
    async editPainting(selected) {
      this.temp.id = selected.id;
      this.temp.title = selected.title;
      this.temp.year = selected.year;
      this.temp.on_display = selected.on_display;

      this.saving = true;
    },
    async savePainting() {
      const response = await fetch(
        `http://127.0.0.1:8000/api/paintings/${this.temp.id}`,
        {
          method: "PATCH",
          headers: {
            "Content-Type": "application/json",
            "Accept": "application/json",
          },
          body: JSON.stringify(this.temp),
        }
      );

      console.log(response);

      await this.getPaintings();

      this.resetTemp();

      this.saving = false;
    },
    async deletePainting(selectedId) {
      const response = await fetch(
        `http://127.0.0.1:8000/api/paintings/${selectedId}`,
        {
          method: "DELETE",
        }
      );

      await this.getPaintings();
      console.log(response);
    },
    async newPainting() {
      const response = await fetch("http://127.0.0.1:8000/api/paintings", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Accept": "application/json",
        },
        body: JSON.stringify(this.temp),
      });

      console.log(response);
      await this.getPaintings();
      this.resetTemp();
    },
    resetTemp() {
      this.temp.id = 0;
      this.temp.title = "";
      this.temp.year = 0;
      this.temp.on_display = false;
    },
  },
  mounted() {
      this.getPaintings()
  }
}

</script>


