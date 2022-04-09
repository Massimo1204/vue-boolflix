<template>
  <header
    class="d-flex justify-content-between align-items-center px-5 py-2 bg-dark border-bottom border-secondary"
  >
    <div>
      <h1 class="text-uppercase" @click="$emit('sendReset', reset++)">
        Boolflix
      </h1>
    </div>
    <div>
      <select
        class="me-3"
        name="movieGenres"
        v-if="genreLists"
        v-model="filterMovieGenre"
        @change="$emit('sendMovieGenre', filterMovieGenre)"
      >
        <option value="all">All Movie Genres</option>
        <option
          v-for="(element, index) in genreLists[0]"
          :key="index + 'movie'"
          :value="element.name"
        >
          {{ element.name }}
        </option>
      </select>
      <select
        class="me-3"
        name="tvSeriesGenres"
        v-if="genreLists"
        v-model="filterSeriesGenre"
        @change="$emit('sendSeriesGenre', filterSeriesGenre)"
      >
        <option value="all">All Series Genres</option>
        <option
          v-for="(element, index) in genreLists[1]"
          :key="index + 'tv'"
          :value="element.name"
        >
          {{ element.name }}
        </option>
      </select>
      <select
        class="me-3 rounded-2 fw-bold"
        name="filterShow"
        v-model="filterShow"
        @change="$emit('sendFilterShow', filterShow)"
      >
        <option value="all">All</option>
        <option value="movie">Movies</option>
        <option value="series">Series</option>
      </select>
      <i class="fas fa-magnifying-glass me-2 text-light"></i>
      <input
        class="rounded-2"
        type="text"
        placeholder="search"
        v-model="toSearch"
        @keyup.enter="$emit('sendSearch', toSearch.trim())"
      />
    </div>
  </header>
</template>

<script>
export default {
  name: "indexHeader",
  props: ["genreLists"],
  data: function () {
    return {
      toSearch: "",
      filterShow: "all",
      filterMovieGenre: "all",
      filterSeriesGenre: "all",
      reset: 0,
    };
  },
};
</script>

<style lang="scss" scoped>
@import "../style/style.scss";

header {
  div {
    h1 {
      color: $logo-red;
      cursor: pointer;
      user-select: none;
    }
  }
}
</style>
