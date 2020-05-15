<template>
  <div>
    <div class="input-group-lg mt-3 px-5 col d-flex justify-content-center">
      <!-- This input should be moved to Main.vue  -->
      <input
        type="text"
        v-model="search"
        @input="handleInput"
        class="rounded form-control text-center w-75"
        placeholder="Search for Marvel characters"
      />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: "",
    };
  },
  methods: {
    handleInput() {
      this.$emit("input", this.search)
    },
  },
};
</script>

<style scoped></style>
