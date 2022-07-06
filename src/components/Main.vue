<template>
  <main class="bg-dark p-3">
    <showCard
      :movies="movies"
      :tvSeries="tvSeries"
      :moviesCasts="moviesCasts"
      :seriesCasts="seriesCasts"
      :toDisplay="toDisplay"
      :genres="genres"
      :loader="loader"
      :filterMovieGenre="filterMovieGenre"
      :filterSeriesGenre="filterSeriesGenre"
      :isStart="isStart"
    />
  </main>
</template>

<script>
import axios from "axios";
import showCard from "./Cards.vue";

export default {
  name: "indexMain",
  props: {
    toSearch: String,
    filterShow: String,
    filterMovieGenre: String,
    filterSeriesGenre: String,
    isReset: Number,
  },
  components: {
    showCard,
  },
  data: function () {
    return {
      apiUrl: "https://api.themoviedb.org/3/",
      ApiKeyUrl: "?api_key=09c2419c715c8b3c902f24ec9586895f",
      seriesCasts: [],
      moviesCasts: [],
      movies: null,
      tvSeries: null,
      loader: false,
      toDisplay: [true, true],
      genres: [[], []],
      genreLists: [[], []],
      shows: ["movie", "tv"],
      isStart: true,
    };
  },
  methods: {
    getApiShows(toSearch, type) {
      let category;
      if (this.isStart || toSearch == "") {
        category = type + "/popular";
      } else {
        category = "search/" + type;
      }
      axios
        .get(this.apiUrl + category + this.ApiKeyUrl + "&query=" + toSearch)
        .then((item) => {
          if (type == "movie") {
            this.movies = item.data.results;
          } else if (type == "tv") {
            this.tvSeries = item.data.results;
          }
          this.getDetails(type);
        })
        .catch((error) => {
          console.error(error);
        });
    },
    getDetails(show) {
      if (show == "movie") {
        this.movies.forEach((element, index) => {
          this.getApiCast("movie/" + element.id + "/credits", "movie", index);
          this.getGenres(element.id, "movie", index, 0);
        });
      } else if (show == "tv") {
        this.tvSeries.forEach((element, index) => {
          this.getApiCast("tv/" + element.id + "/credits", "series", index);
          this.getGenres(element.id, "tv", index, 1);
        });
      }
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
    getGenres(id, type, index, i) {
      axios
        .get(this.apiUrl + type + "/" + id + this.ApiKeyUrl)
        .then((item) => {
          this.genres[i][index] = item.data.genres;
        })
        .catch((error) => {
          console.error(error);
        });
    },
    getGenreList(type, i) {
      axios
        .get(this.apiUrl + "genre/" + type + "/list" + this.ApiKeyUrl)
        .then((item) => {
          this.genreLists[i] = item.data.genres;
        })
        .catch((error) => {
          console.error(error);
        });
    },
    startLoader() {
      this.loader = false;
      setTimeout(() => {
        this.loader = true;
      }, 700);
    },
  },
  watch: {
    toSearch(toSearch) {
      this.isStart = false;
      this.startLoader();
      this.movies = null;
      this.tvSeries = null;
      this.shows.forEach((element) => {
        this.getApiShows(toSearch, element);
      });
    },
    filterShow(filterShow) {
      switch (filterShow) {
        case "movie":
          this.toDisplay = [true, false];
          break;
        case "series":
          this.toDisplay = [false, true];
          break;
        case "all":
          this.toDisplay = [true, true];
          break;
        default:
          this.toDisplay = [true, true];
          break;
      }
    },
    isReset() {
      this.startLoader();
      this.isStart = true;
      this.shows.forEach((element) => {
        this.getApiShows("", element);
      });
    },
  },
  mounted() {
    setTimeout(() => {
      this.$emit("sendGenreLists", this.genreLists);
      this.loader = true;
    }, 700);
    this.shows.forEach((element, index) => {
      this.getApiShows("", element);
      this.getGenreList(element, index);
    });
  },
};
</script>

<style scoped lang="scss">
main {
  min-height: calc(100vh - 73px);
}
</style>
