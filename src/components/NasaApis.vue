<template>
  <div>
    <v-container>
      <AsteroidsGrid @remove="remove" :asteroids="asteroids" header="Near-Earth Objects" />
    </v-container>
  </div>
</template>

<script>
import axios from "axios";
import AsteroidsGrid from "./AsteroidsGrid.vue";

export default {
  name: "NasaApis",
  components: {
    AsteroidsGrid
  },
  data() {
    return {
      api_url: "https://api.nasa.gov/neo/rest/v1/neo/browse?api_key=",
      api_key: process.env.VUE_APP_API_KEY,
      apod: null,
      asteroids: [],
      headers: ["#", "Name", "Close Approach Date", "Miss Distance"]
    };
  },
  computed: {
    apod_url: function() {
      return `${this.api_url}${this.api_key}`;
    }
  },
  async created() {
    this.fetchAsteroids();
  },
  methods: {
    fetchAsteroids: function() {
      var url = this.api_url + this.api_key;
      axios.get(url).then(res => {
        this.asteroids = res.data.near_earth_objects.slice(0, 10);
      });
    },
    remove: function(index) {
      this.asteroids.splice(index, 1);
    }
  }
};
</script>
<style></style>
