<template>
  <main>
    <showCard :show="movies" />
  </main>
</template>

<script>
import axios from "axios";
import showCard from "./Card.vue";

export default {
  name: "indexMain",
  props: { toSearch: String },
  components: {
    showCard,
  },
  data: function () {
    return {
      moviesApiUrl:
        "https://api.themoviedb.org/3/search/movie?api_key=09c2419c715c8b3c902f24ec9586895f&query=",
      flagsApiUrl: "https://countryflagsapi.com/png/",
      movies: null,
    };
  },
  methods: {
    getApiMovies(url, toSearch) {
      axios.get(url + toSearch).then((item) => {
        this.movies = item.data.results;
      })
      .catch(error => {
        console.error(error);
      });
    },
  },
  watch: {
    toSearch(toSearch) {
      this.getApiMovies(this.moviesApiUrl, toSearch);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
