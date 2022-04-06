<template>
<div>
  <div>
    <h1 class="ms-3 pt-3 mb-0">Movies</h1>
  </div>
  <div class="d-flex justify-content-start flex-wrap">
    <div
      class="my-card"
      v-for="(element, index) in movies"
      :key="index"
      @mouseover="toShowId = element.id"
      @mouseover.once="overviewHeight(index)"
      @mouseleave="toShowId = null"
    >
      <div v-show="toShowId == element.id" ref="cardBack">
        <h6 class="card-title" ref="title">
          Titolo:
          <span>{{ element.title }}</span>
        </h6>
        <h6 class="card-title" ref="originalTitle">
          Titolo originale:
          <span>{{ element.original_title }}</span>
        </h6>
        <div>
          <h6 class="card-rating m-0" ref="rating">
            Rating:
            <i
              class="fas fa-star text-warning"
              v-for="n in rankingStars(element.vote_average)"
              :key="n"
            ></i>
            <i
              class="fas fa-star-half text-warning"
              v-if="halfStar(element.vote_average) == true"
            ></i>
          </h6>
        </div>
        <div>
          <h6 class="card-language d-flex align-items-center" ref="language">
            Language:
            <country-flag :country="langToCountry(element.original_language)" />
          </h6>
        </div>
        <h6 class="card-overview m-0" ref="overview">
          Overview:
          <span>{{ element.overview }}</span>
        </h6>
      </div>
      <div v-show="toShowId != element.id">
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
</div>
</template>

<script>
export default {
  name: "cardMovies",
  props: [
    "movies",
    "apiImgUrl",
    "rankingStars",
    "halfStar",
    "langToCountry",
    ],
  data: function () {
    return {
      toShowId: null,
    };
  },
  methods:{
    overviewHeight(index) {
      this.$refs.overview[index].style.height = 275 - (this.$refs.title[index].clientHeight+this.$refs.originalTitle[index].clientHeight+this.$refs.rating[index].clientHeight+this.$refs.language[index].clientHeight)+ 'px';
    },
  },
};
</script>

<style></style>
