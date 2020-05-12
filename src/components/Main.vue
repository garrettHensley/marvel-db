<template>
  <div class="home">
    <p class="display-4">{{ Search }}</p>

    <div>
      <b-list-group>
        <div v-for="(character, index) in info" :key="character.id">
          <b-list-group-item class="bg-info">
            {{ character.name }}
          </b-list-group-item>
          <b-list-group-item v-if="showDesc(index)" class="bg-dark text-light">
            {{ character.description }}
          </b-list-group-item>
        </div>
      </b-list-group>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Home",
  components: {},
  data() {
    return {
      info: null,
      publicKey: "4327819a4e9ae453434bb3d2dcc52456",
      time: 1564731162583,
    };
  },
  props: {
    searchName: String,
  },
  mounted() {
    this.getUrl();
  },
  methods: {
    getUrl() {
      console.log("you suck!!!!");
      if (this.Search) {
        axios
          .get(
            `http://gateway.marvel.com/v1/public/characters?&nameStartsWith=${
              this.Search
            }&ts=1&apikey=${
              this.publicKey
            }&hash=${"4dfd3313409d3a26b9513377ea1c2698".toLowerCase()}`
          )
          .then((response) => (this.info = response.data.data.results));
      } else {
        axios
          .get(
            `http://gateway.marvel.com/v1/public/characters?&ts=1&apikey=${
              this.publicKey
            }&hash=${"4dfd3313409d3a26b9513377ea1c2698".toLowerCase()}`
          )
          .then((response) => (this.info = response.data.data.results));
      }
    },
    showDesc() {},
  },
  watch: {
    searchName: function() {
      console.log("you suck!!!!");
      if (this.Search) {
        axios
          .get(
            `http://gateway.marvel.com/v1/public/characters?&nameStartsWith=${
              this.Search
            }&ts=1&apikey=${
              this.publicKey
            }&hash=${"4dfd3313409d3a26b9513377ea1c2698".toLowerCase()}`
          )
          .then((response) => (this.info = response.data.data.results));
      } else {
        axios
          .get(
            `http://gateway.marvel.com/v1/public/characters?&ts=1&apikey=${
              this.publicKey
            }&hash=${"4dfd3313409d3a26b9513377ea1c2698".toLowerCase()}`
          )
          .then((response) => (this.info = response.data.data.results));
      }
    },
  },
  computed: {
    Search() {
      return this.searchName;
    },
  },
};
</script>
