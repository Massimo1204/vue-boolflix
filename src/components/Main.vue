<template>
  <main class="bg-dark">
    <showCard
      :movies="movies"
      :tvSeries="tvSeries"
      :moviesCasts="moviesCasts"
      :seriesCasts="seriesCasts"
    />
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
      apiUrl: "https://api.themoviedb.org/3/",
      ApiKeyUrl: "?api_key=09c2419c715c8b3c902f24ec9586895f&language=it_IT",
      seriesCasts: [],
      moviesCasts: [],
      movies: null,
      tvSeries: null,
    };
  },
  methods: {
    getApiMovies(toSearch) {
      axios
        .get(this.apiUrl + "search/movie" + this.ApiKeyUrl + toSearch)
        .then((item) => {
          this.movies = item.data.results;
          this.movies.forEach((element, index) => {
            this.getApiCast("movie/" + element.id + "/credits", "movie", index);
          });
        })
        .catch((error) => {
          console.error(error);
        });
    },
    getApiTvSeries(toSearch) {
      axios
        .get(this.apiUrl + "search/tv" + this.ApiKeyUrl + toSearch)
        .then((item) => {
          this.tvSeries = item.data.results;
          this.tvSeries.forEach((element, index) => {
            this.getApiCast("tv/" + element.id + "/credits", "series", index);
          });
        })
        .catch((error) => {
          console.error(error);
        });
    },
    getApiCast(id, show, index) {
      axios
        .get(this.apiUrl + id + this.ApiKeyUrl)
        .then((item) => {
          if (show == "movie") {
            this.moviesCasts[index] = item.data.cast.slice(0, 5);
          } else if (show == "series") {
            this.seriesCasts[index] = item.data.cast.slice(0, 5);
          }
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

<style scoped lang="scss">
main {
  min-height: calc(100vh - 72px);
}
</style>
