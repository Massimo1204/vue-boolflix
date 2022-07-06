<template>
  <div>
    <div v-if="joinShows && loader">
      <div
        class="position-relative"
        v-for="(show, showIndex) in joinShows"
        :key="showIndex"
        v-show="toDisplay[showIndex]"
      >
        <div>
          <h1
            class="pt-4 pb-2 ms-2 text-capitalize"
            :class="!isStart ? 'text-center' : ''"
          >
            {{ shows[showIndex] }}
          </h1>
        </div>
        <div
          class="cards-container d-flex justify-content-start gap-3"
          :class="isStart ? 'carousel' : 'flex-wrap justify-content-center'"
        >
          <div
            class="my-card"
            :class="!isStart ? 'me-1 mb-1' : ''"
            v-for="(element, index) in show"
            :key="index + shows[showIndex] + element.id"
            @mouseover="toShowId = element.id"
            @mouseover.once="overviewHeight(showIndex, index)"
            @mouseleave="toShowId = null"
            v-show="toFilter(showIndex, index)"
          >
            <div v-show="toShowId == element.id" class="my-card" ref="cardBack">
              <h6 class="card-title" ref="title">
                Title:
                <span>{{ getTitle(showIndex, index) }}</span>
              </h6>
              <div>
                <h6 class="card-rating m-0" ref="rating">
                  Rating:
                  <i
                    class="fas fa-star text-warning"
                    v-for="n in rankingStars(element.vote_average)"
                    :key="n + 'fullStar' + index"
                  ></i>
                  <i
                    class="fa-regular fa-star-half-stroke text-warning"
                    v-if="halfStar(element.vote_average)"
                  ></i>
                  <i
                    class="fa-regular fa-star text-warning"
                    v-for="n in 5 -
                    (rankingStars(element.vote_average) +
                      (halfStar(element.vote_average) ? 1 : 0))"
                    :key="n + 'emptyStar' + index"
                  ></i>
                </h6>
              </div>
              <div>
                <h6
                  class="card-language d-flex align-items-center"
                  ref="language"
                >
                  Language:
                  <country-flag
                    :country="langToCountry(element.original_language)"
                  />
                </h6>
              </div>
              <div v-if="joinCasts[showIndex].length != 0">
                <h6 class="cast" ref="cast">
                  Cast:
                  <span
                    v-for="n in joinCasts[showIndex][index].length"
                    :key="n"
                  >
                    {{
                      joinCasts[showIndex][index][n - 1].name +
                      (n == joinCasts[showIndex][index].length ? "" : ", ")
                    }}
                  </span>
                </h6>
              </div>
              <div v-if="genres[showIndex][index]">
                <h6 class="genres" ref="genres">
                  Genres:
                  <span v-for="n in genres[showIndex][index].length" :key="n">{{
                    genres[showIndex][index][n - 1].name +
                    (n == genres[showIndex][index].length ? "" : ", ")
                  }}</span>
                </h6>
              </div>
              <div>
                <h6 class="card-overview m-0" ref="overview">
                  Overview:
                  <span>{{ element.overview }}</span>
                </h6>
              </div>
            </div>
            <div v-show="toShowId != element.id">
              <img
                v-if="element.poster_path"
                :src="apiImgUrl + element.poster_path"
                :alt="getTitle(showIndex, index)"
              />
              <div v-else>
                <img
                  src="data:image/png;base64,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kKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAgBBQkp2piMgIIwbk6FEFCQkKKNyQgoCOPmVAiB/wOhwSjXzNE15wAAAABJRU5ErkJggg=="
                  alt="Not Available"
                />
              </div>
            </div>
          </div>
        </div>
        <div
          v-if="isStart"
          class="carousel-buttons-container"
          @mouseover="displayCarouselButtons = true"
          @mouseleave="displayCarouselButtons = false"
        >
          <div class="carousel-buttons-wrapper">
            <div
              v-if="displayCarouselButtons"
              class="previous-button"
              @click="scrollBack()"
            >
              <i class="fas fa-chevron-left"></i>
            </div>
            <div
              v-if="displayCarouselButtons"
              class="next-button"
              @click="scrollForward()"
            >
              <i class="fas fa-chevron-right"></i>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-else>
      <h1 class="text-center m-5">Loading...</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: "showCard",
  props: [
    "movies",
    "tvSeries",
    "moviesCasts",
    "seriesCasts",
    "toDisplay",
    "genres",
    "loader",
    "filterMovieGenre",
    "filterSeriesGenre",
    "isStart",
  ],
  data: function () {
    return {
      apiImgUrl: "https://image.tmdb.org/t/p/w500",
      toShowId: null,
      displayCarouselButtons: null,
      carousel: null,
    };
  },
  methods: {
    toFilter(showIndex, index) {
      if (showIndex == 0) {
        if (this.filterMovieGenre == "all") {
          return true;
        } else {
          return this.genres[showIndex][index].some(
            (element) => element.name == this.filterMovieGenre
          );
        }
      } else if (showIndex == 1) {
        if (this.filterSeriesGenre == "all") {
          return true;
        } else {
          return this.genres[showIndex][index].some(
            (element) => element.name == this.filterSeriesGenre
          );
        }
      }
    },
    getTitle(showIndex, index) {
      if (showIndex == 0) {
        return this.joinShows[0][index].title;
      } else {
        return this.joinShows[1][index].name;
      }
    },
    overviewHeight(showIndex, index) {
      let i;
      if (showIndex == 0) {
        i = index;
      } else {
        i = index + this.movies.length;
      }
      this.$refs.overview[i].style.height =
        275 -
        (this.$refs.title[i].clientHeight +
          this.$refs.rating[i].clientHeight +
          this.$refs.language[i].clientHeight +
          this.$refs.cast[i].clientHeight +
          this.$refs.genres[i].clientHeight) +
        "px";
    },
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
      switch (lang) {
        case "en":
          return "gb";
        case "ja":
          return "jp";
        case "hi":
          return "in";
        case "da":
          return "dk";
        case "fa":
          return "ir";
        case "ur":
          return "pk";
        case "uk":
          return "ua";
        case "sq":
          return "al";
        case "zh":
          return "cn";
        case "ko":
          return "kp";
        case "el":
          return "gr";
        case "cs":
          return "cz";
        case "ta":
          return "lk";
        case "xx":
          return "un";
        case "te":
          return "in";
        default:
          return lang;
      }
    },
    scrollForward() {
      this.carousel = document.getElementsByClassName("cards-container");
      this.carousel[0].scrollBy({
        left: window.innerWidth - 200,
        top: 0,
        behavior: "smooth",
      });
    },
    scrollBack() {
      this.carousel = document.getElementsByClassName("cards-container");
      this.carousel[0].scrollBy({
        left: -window.innerWidth + 200,
        top: 0,
        behavior: "smooth",
      });
    },
  },
  computed: {
    joinShows: function () {
      if (this.movies && this.tvSeries) {
        return [this.movies, this.tvSeries];
      } else {
        return null;
      }
    },
    joinCasts: function () {
      return [this.moviesCasts, this.seriesCasts];
    },
    shows: function () {
      if (this.isStart) {
        return ["Popular Movies", "Popular Series"];
      } else {
        return ["Movies", "Tv Series"];
      }
    },
  },
};
</script>

<style lang="scss" scoped>
div.carousel {
  width: calc(100vw - 2rem);
  overflow-x: scroll;
  scrollbar-width: none;
  -ms-overflow-style: none;
}
.carousel::-webkit-scrollbar {
  display: none;
}
div.carousel-buttons-container {
  position: absolute;
  width: 100%;
  height: 100%;
  top: calc(80px + 0.5rem);
  right: 0;
}
div.carousel-buttons-wrapper {
  position: relative;
}
div.next-button,
div.previous-button {
  position: absolute;
  height: 300px;
  width: 50px;
  background-color: rgba($color: #000000, $alpha: 0.25);
  font-size: 2.2rem;
  color: white;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}
div.next-button {
  right: 0;
}
div.previous-button {
  left: 0;
}
</style>
