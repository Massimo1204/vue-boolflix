<template>
  <main>
    <div>
      {{ items }}
    </div>
  </main>
</template>

<script>
import axios from "axios";

export default {
  name: "indexMain",
  props: { toSearch: String },
  data: function () {
    return {
      apiUrl:
        "https://api.themoviedb.org/3/search/movie?api_key=09c2419c715c8b3c902f24ec9586895f&query=",
      items: null,
    };
  },
  methods: {
    getApiItems(url, toSearch) {
      axios.get(url + toSearch).then((item) => {
        this.items = item.data.results;
      });
    },
  },
  watch: {
    toSearch(toSearch) {
      this.getApiItems(this.apiUrl, toSearch);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss"></style>
