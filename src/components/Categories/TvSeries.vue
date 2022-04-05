<template>
  <div>
    <div
      class="my-card"
      v-for="(element, index) in tvSeries"
      :key="index"
      @mouseover="toShowId = element.id"
      @mouseleave="toShowId = null"
    >
      <div v-if="toShowId == element.id">
        <h4>{{ element.name }}</h4>
        <h4>{{ element.original_name }}</h4>
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
          class="img-fluid"
          :src="apiImgUrl + element.poster_path"
          :alt="element.name"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "cardTvSeries",
  props: ["tvSeries", "apiImgUrl", "rankingStars", "halfStar", "langToCountry"],
  data: function () {
    return {
      toShowId: null,
    }
  },
};
</script>

<style></style>
