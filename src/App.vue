<template>
  <div id="app">
    <indexHeader
      @sendSearch="copySearch"
      @sendFilterShow="copyFilterShow"
      :genreLists="genreLists"
      @sendMovieGenre="copyMovieGenre"
      @sendSeriesGenre="copySeriesGenre"
      @sendReset="copyReset"
    />
    <indexMain
      :toSearch="toSearch"
      :filterShow="filterShow"
      @sendGenreLists="copyGenreLists"
      :filterMovieGenre="filterMovieGenre"
      :filterSeriesGenre="filterSeriesGenre"
      :isReset="isReset"
    />
  </div>
</template>

<script>
import indexMain from "./components/Main.vue";
import indexHeader from "./components/Header.vue";

export default {
  name: "App",
  components: {
    indexMain,
    indexHeader,
  },
  data: function () {
    return {
      toSearch: "",
      filterShow: "",
      genreLists: null,
      filterMovieGenre: "all",
      filterSeriesGenre: "all",
      isReset: null,
    };
  },
  methods: {
    copySearch(search) {
      this.toSearch = search.toLowerCase();
    },
    copyFilterShow(filterShow) {
      this.filterShow = filterShow;
    },
    copyGenreLists(genres) {
      this.genreLists = genres;
    },
    copyMovieGenre(genre) {
      this.filterMovieGenre = genre;
    },
    copySeriesGenre(genre) {
      this.filterSeriesGenre = genre;
    },
    copyReset(reset) {
      this.isReset = reset;
    },
  },
};
</script>

<style lang="scss">
@import "./style/style.scss";

#app {
  color: white;
}
</style>
