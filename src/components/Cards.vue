<template>
  <div>
    <cardMovies
      :movies="movies"
      :apiImgUrl="apiImgUrl"
      :rankingStars="rankingStars"
      :halfStar="halfStar"
      :langToCountry="langToCountry"
    />
    <h1 class="ms-3 mt-3" v-if="tvSeries">Tv Series</h1>
    <cardTvSeries
      :tvSeries="tvSeries"
      :apiImgUrl="apiImgUrl"
      :rankingStars="rankingStars"
      :halfStar="halfStar"
      :langToCountry="langToCountry"
    />
  </div>
</template>

<script>
import cardMovies from "./Categories/Movies.vue";
import cardTvSeries from "./Categories/TvSeries.vue";

export default {
  name: "mainCard",
  props: ["movies", "tvSeries"],
  components: {
    cardMovies,
    cardTvSeries,
  },
  data: function () {
    return {
      apiImgUrl: "https://image.tmdb.org/t/p/w500",
    };
  },
  methods: {
    rankingStars(vote) {
      vote = Math.ceil(vote);
      if (vote % 2 == 0) {
        return vote / 2;
      } else {
        return Math.floor(vote / 2);
      }
    },
    halfStar(vote) {
      if (Math.ceil(vote) % 2 != 0) {
        return true;
      }
    },
    langToCountry(lang) {
      if (lang == "en") {
        return "gb";
      } else if (lang == "ja") {
        return "jp";
      } else if (lang == "hi") {
        return "in";
      } else if (lang == "da") {
        return "dk";
      } else if (lang == "fa") {
        return "ir";
      } else if (lang == "ur") {
        return "pk";
      } else if (lang == "uk") {
        return "ua";
      } else if (lang == "sq") {
        return "al";
      } else if (lang == "zh") {
        return "cn";
      } else if (lang == "ko") {
        return "kp";
      } else if (lang == "el") {
        return "gr";
      } else if (lang == "cs") {
        return "cz";
      } else if (lang == "ta") {
        return "lk";
      } else if (lang == "xx") {
        return "un";
      } else if (lang == "te") {
        return "in";
      } else {
        return lang;
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
