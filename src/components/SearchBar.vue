<template>
  <input
    type="text"
    v-model="searchedKeyword"
    placeholder="Search by name"
    @input="searchByName"
  />
</template>

<script>
export default {
  data() {
    return {
      searchedKeyword: "",
    };
  },
  methods: {
    searchByName() {
      this.$emit("search", this.searchedKeyword);
    },
  },
};
</script>

<style scoped></style>
