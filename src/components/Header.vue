<template>
  <header>
    <div>
      <input
        type="text"
        placeholder="search"
        v-model="toSearch"
        @keyup.enter="$emit('copySearch', toSearch)"
      />
    </div>
  </header>
</template>

<script>
export default {
  name: "indexHeader",
};
</script>

<style></style>
