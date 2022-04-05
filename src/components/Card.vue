<template>
  <div class="d-flex flex-wrap justify-content-between">
    <div class="my-card" v-for="(element, index) in movies" :key="index" @mouseover="toShowId=element.id" @mouseleave="toShowId = null">
      <div v-if="toShowId==element.id">
        <h4>{{ element.title }}</h4>
        <h4>{{ element.original_title }}</h4>
        <country-flag :country="langToCountry(element.original_language)" />
        <h2>{{ element.vote_average }}</h2>
      </div>
      <div v-else>
        <img
          class="img-fluid"
          :src="apiUrl + element.poster_path" 
          :alt="element.title + ' cover'" 
        />
      </div>
    </div>
    <div class="my-card" v-for="(element, index) in tvSeries" :key="index+1*3.14" @mouseover="toShowId=element.id" @mouseleave="toShowId = null">
      <div v-if="toShowId==element.id">
        <h4>{{ element.name }}</h4>
        <h4>{{ element.original_name }}</h4>
        <country-flag :country="langToCountry(element.original_language)" />
        <h2>{{ element.vote_average }}</h2>
      </div>
      <div v-else>
        <img
          class="img-fluid"
          :src="apiUrl + element.poster_path" 
          :alt="element.title + ' cover'" 
        />
      </div>
    </div>
  </div>
</template>

<script>
import CountryFlag from "vue-country-flag";
export default {
  name: "mainCard",
  props: ["movies", "tvSeries"],
  components: {
    CountryFlag,
  },
  data: function () {
    return {
      apiUrl: "https://image.tmdb.org/t/p/w500",
      toShow: false,
      toShowId: null,
    }
  },
  methods: {
    langToCountry(lang) {
      if(lang == 'en') {
        return 'gb';
      }
      else if(lang == 'ja') {
        return 'jp';
      }
      else if (lang == 'hi'){
        return 'in';
      }
      else if(lang == 'da'){
        return 'dk';
      }
      else if(lang =='fa'){
        return 'ir';
      }
      else if(lang == 'ur'){
        return 'pk';
      }
      else if(lang == 'uk'){
        return 'ua';
      }
      else if(lang == 'sq'){
        return 'al';
      }
      else if(lang == 'zh'){
        return 'cn';
      }
      else if(lang == 'ko'){
        return 'kp';
      }
      else if(lang == 'el'){
        return 'gr';
      }
      else if(lang == 'cs'){
        return 'cz';
      }
      else if(lang == 'ta'){
        return 'lk';
      }
      else if(lang == 'xx'){
        return 'un';
      }
      else if(lang == 'te'){
        return 'in';
      }
      else {
        return lang;
      } 
    },
  },
};
</script>

<style lang="scss" scoped>
div {
  div.my-card {
    width: 200px;
    height: 450px;
  }
}
</style>
