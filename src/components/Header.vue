<template>
  <header
    class="d-flex justify-content-between align-items-center p-2 bg-dark border-bottom border-secondary"
  >
    <div>
      <h1 class="text-uppercase text-danger">Boolflix</h1>
    </div>
    <div class="me-4">
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

<style></style>
