<template>
  <main>
    <showCard :movies="movies" :tvSeries="tvSeries" />
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
      tvSeriesApiUrl:
        "https://api.themoviedb.org/3/search/tv?api_key=09c2419c715c8b3c902f24ec9586895f&query=",
      movies: null,
      tvSeries:null,
    };
  },
  methods: {
    getApiItems(url, toSearch, checker) {
      axios.get(url + toSearch).then((item) => {
        if(checker){
          this.movies = item.data.results;
          console.log(this.movies);
        }
        else {
          this.tvSeries = item.data.results;
          console.log(this.tvSeries);
        }
      })
      .catch(error => {
        console.error(error);
      });
    },
  },
  watch: {
    toSearch(toSearch) {
      this.getApiItems(this.moviesApiUrl, toSearch, true);
      this.getApiItems(this.tvSeriesApiUrl, toSearch, false);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
