<template>
  <div class="d-flex justify-content-start flex-wrap">
    <div
      class="my-card"
      v-for="(element, index) in movies"
      :key="index"
      @mouseover="toShowId = element.id"
      @mouseleave="toShowId = null"
    >
      <div v-if="toShowId == element.id">
        <h4>{{ element.title }}</h4>
        <h4>{{ element.original_title }}</h4>
        <country-flag :country="langToCountry(element.original_language)" />
        <div>
          <i
            class="fas fa-star"
            v-for="n in rankingStars(element.vote_average)"
            :key="n"
          ></i>
          <i
            class="fas fa-star-half"
            v-if="halfStar(element.vote_average) == true"
          ></i>
        </div>
      </div>
      <div v-else>
        <img
          v-if="element.poster_path"
          :src="apiImgUrl + element.poster_path"
          :alt="element.title"
        />
        <div v-else>
          <h3>{{ element.title }}</h3>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "cardMovies",
  props: ["movies", "apiImgUrl", "rankingStars", "halfStar", "langToCountry"],
  data: function () {
    return {
      toShowId: null,
    }
  },
};
</script>

<style></style>
