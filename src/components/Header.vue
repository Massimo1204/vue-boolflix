<template>
  <header>
    <div>
      <input
        type="text"
        placeholder="search"
        v-model="toSearch"
        @keyup.enter="$emit('sendSearch', toSearch)"
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
