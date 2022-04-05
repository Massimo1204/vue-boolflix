<template>
  <div class="d-flex flex-wrap justify-content-between">
    <div class="card" v-for="(element, index) in movies" :key="index">
      <h1>{{ element.title }}</h1>
      <h1>{{ element.original_title }}</h1>
      <country-flag :country="langToCountry(element.original_language)" />
      <h2>{{ element.vote_average }}</h2>
    </div>
    <h1>serie tv</h1>
    <div class="card" v-for="(element, index) in tvSeries" :key="index+1*3.14">
      <h1>{{ element.name }}</h1>
      <h1>{{ element.original_name }}</h1>
      <country-flag :country="langToCountry(element.original_language)" />
      <h2>{{ element.vote_average }}</h2>
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

<style></style>
