<template>
  <div>
    <h1></h1>
    <div class="row bg-dark text-warning py-3">
      <div class="col d-flex justify-content-center align-items-center">
        <div>
          <h1 class="display-1">{{ Name }}</h1>
        </div>
      </div>
      <div class="col">
        <img :src="Pic" class="fluid img-thumbnail w-50 rounded-circle" />
      </div>
    </div>
    <div class="row">
      <div v-for="comic in info" :key="comic.id">
        <!-- MAKE ALL OF THIS INSIDE HERE A COMPONENT Comic.vue -->
        <p class="lead font-italic">{{ comic.title }}</p>
        <Comic
          :title="comic.title"
          :image="comic.thumbnail.path + '.' + comic.thumbnail.extension"
          :description="comic.description"
          :creators="comic.creators.items"
          :characters="comic.characters.items"
          class="p-4"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Comic from "@/components/Comic.vue";

export default {
  components: {
    Comic,
  },
  props: {
    characterId: Number,
    Name: String,
    Pic: String,
    description: String,
  },
  data() {
    return {
      info: null,
      hash: "4dfd3313409d3a26b9513377ea1c2698",
      publicKey: "4327819a4e9ae453434bb3d2dcc52456",
      time: 1,
    };
  },
  mounted() {
    this.getUrl();
  },
  methods: {
    getUrl() {
      axios
        .get(
          `https://gateway.marvel.com/v1/public/characters/${this.characterId}/comics?apikey=4327819a4e9ae453434bb3d2dcc52456&ts=1&hash=4dfd3313409d3a26b9513377ea1c2698`
        )
        .then((response) => (this.info = response.data.data.results));
      console.log(
        `https://gateway.marvel.com/v1/public/characters/${this.characterId}/comics?apikey=4327819a4e9ae453434bb3d2dcc52456&ts=1&hash=4dfd3313409d3a26b9513377ea1c2698`
      );
    },
  },
};
</script>

<style scoped></style>
