<template>
  <div class="d-flex flex-wrap justify-content-between">
    <div class="card" v-for="(element, index) in movies" :key="index">
      <h1>{{ element.title }}</h1>
      <h1>{{ element.original_title }}</h1>
      <img :src="'https://countryflagsapi.com/png/' + ((element.original_language == 'en') ? 'usa' : element.original_language)" alt="">
      <h2>{{ element.vote_average }}</h2>
    </div>
    <h1>serie tv</h1>
    <div class="card" v-for="(element, index) in tvSeries" :key="index+1*3.14">
      <h1>{{ element.name }}</h1>
      <h1>{{ element.original_name }}</h1>
      <img :src="'https://countryflagsapi.com/png/' + ((element.original_language == 'en') ? 'usa' : element.original_language)" alt="">
      <h2>{{ element.vote_average }}</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: "mainCard",
  props: ["movies", "tvSeries"],
};
</script>

<style></style>
