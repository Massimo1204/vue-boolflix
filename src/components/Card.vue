<template>
  <div class="d-flex flex-wrap justify-content-between">
    <div class="card" v-for="(element, index) in show" :key="index">
      <h1>{{ element.title }}</h1>
      <h1>{{ element.original_title }}</h1>
      <img :src="'https://countryflagsapi.com/png/' + ((element.original_language == 'en') ? 'usa' : element.original_language)" alt="">
      <h2>{{ element.vote_average }}</h2>
    </div>
  </div>
</template>

<script>
export default {
  name: "mainCard",
  props: ["show"],
};
</script>

<style></style>
