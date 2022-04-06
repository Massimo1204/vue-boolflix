<template>
  <div class="d-flex justify-content-start flex-wrap">
    <div
      class="my-card"
      v-for="(element, index) in tvSeries"
      :key="index"
      @mouseover="toShowId = element.id"
      @mouseleave="toShowId = null"
    >
      <div v-if="toShowId == element.id">
        <h6 class="card-title">
          Titolo:
          <span>{{ element.name }}</span>
        </h6>
        <h6 class="card-title">
          Titolo originale:
          <span>{{ element.original_name }}</span>
        </h6>
        <div>
          <h6 class="card-rating">
            Rating:
            <i
              class="fas fa-star"
              v-for="n in rankingStars(element.vote_average)"
              :key="n"
            ></i>
            <i
              class="fas fa-star-half"
              v-if="halfStar(element.vote_average) == true"
            ></i>
          </h6>
        </div>
        <div>
          <h6 class="card-language">
            Language:
            <country-flag :country="langToCountry(element.original_language)" />
          </h6>
        </div>
        <h6 class="card-overview">
          Overview:
          <span>{{ element.overview }}</span>
        </h6>
      </div>
      <div v-else>
        <img
          v-if="element.poster_path"
          :src="apiImgUrl + element.poster_path"
          :alt="element.name"
        />
        <div v-else>
          <h3>{{ element.name }}</h3>
        </div>
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
    };
  },
};
</script>

<style></style>
