<template>
  <div class="home">
    <input type="text" v-model="search" @keyup.enter="commitSearch" />
      <Main :searchName="search" />

    {{ search }}
  </div>
</template>

<script>
import Main from "@/components/Main.vue";

export default {
  components: {
    Main,
  },
  data() {
    return {
      search: "spid",
      searchList: [],
    };
  },
};
</script>
