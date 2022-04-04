<template>
  <main>
    {{ movies }}
  </main>
</template>

<script>
import axios from "axios";

export default {
  name: "indexMain",
  props: ["toSearch"],
  data: function () {
    return {
      apiUrl:
        "https://api.themoviedb.org/3/search/movie?api_key=09c2419c715c8b3c902f24ec9586895f&query=back",
      movies: null,
    };
  },
  methods: {
    getApiItems(url) {
      axios.get(url).then((item) => {
        this.movies = item.data.results;
      });
    },
  },
  created: function () {
    this.getApiItems(this.apiUrl);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
