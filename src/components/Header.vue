<template>
  <header
    class="d-flex justify-content-between align-items-center px-3 py-2 bg-dark border-bottom border-secondary"
  >
    <div>
      <h1 class="text-uppercase">Boolflix</h1>
    </div>
    <div class="me-3">
      <i class="fas fa-magnifying-glass me-2 text-light"></i>
      <input
        class="rounded-2"
        type="text"
        placeholder="search"
        v-model="toSearch"
        @change="$emit('sendSearch', toSearch)"
      />
    </div>
  </header>
</template>

<script>
export default {
  name: "indexHeader",
  data: function () {
    return {
      toSearch: "",
    };
  },
};
</script>

<style lang="scss" scoped>
@import "../style/style.scss";

header {
  div {
    h1 {
      color: $logo-red;
    }
  }
}

</style>
