<template>
  <div id="app">
    <indexHeader :copySearch="search" />
    <indexMain @toSearch="toSearch" />
  </div>
</template>

<script>
import indexMain from "./components/Main.vue";
import indexHeader from "./components/Header.vue";

export default {
  name: "App",
  components: {
    indexMain,
    indexHeader,
  },
  data: function () {
    return {
      toSearch: "",
    };
  },
  methods: {
    copySearch(search) {
      this.toSearch = search;
    },
  },
};
</script>

<style lang="scss">
@import "./style/style.scss";

#app {
  text-align: center;
}
</style>
