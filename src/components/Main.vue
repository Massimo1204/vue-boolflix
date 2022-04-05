<template>
  <main class="bg-dark">
    <showCard :movies="movies" :tvSeries="tvSeries" />
  </main>
</template>

<script>
import axios from "axios";
import showCard from "./Cards.vue";

export default {
  name: "indexMain",
  props: { toSearch: String },
  components: {
    showCard,
  },
  data: function () {
    return {
      apiUrl: "https://api.themoviedb.org/3/search/",
      ApiKeyUrl:
        "?api_key=09c2419c715c8b3c902f24ec9586895f&language=it_IT&query=",
      movies: null,
      tvSeries: null,
    };
  },
  methods: {
    getApiMovies(toSearch) {
      axios
        .get(this.apiUrl + "movie" + this.ApiKeyUrl + toSearch)
        .then((item) => {
          this.movies = item.data.results;
          console.log(this.movies);
        })
        .catch((error) => {
          console.error(error);
        });
    },
    getApiTvSeries(toSearch) {
      axios
        .get(this.apiUrl + "tv" + this.ApiKeyUrl + toSearch)
        .then((item) => {
          this.tvSeries = item.data.results;
          console.log(this.tvSeries);
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
  watch: {
    toSearch(toSearch) {
      this.getApiMovies(toSearch);
      this.getApiTvSeries(toSearch);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
main {
  min-height: calc(100vh - 72px);
}
</style>
