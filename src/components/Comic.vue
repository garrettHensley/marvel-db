<template>
  <div class="d-flex">
    <div class="col-8">
      <img :src="image" @click="fullView = !fullView" class="img-fluid" />
    </div>
    <div v-if="fullView" class="bg-dark text-light col">
      <p class="lead font-italic">{{ title }}</p>
      <p>{{ description }}</p>
      <ul>
        Created by:
        <span v-for="creator in creators" :key="creator.id">
          <li
            v-if="
              creator.role == 'writer' ||
                creator.role == 'colorist' ||
                creator.role == 'inker'
            "
          >
            {{ creator.role }}:
            {{ creator.name }}
          </li>
        </span>
      </ul>
      <p>Features:</p>
      <p>
        <span v-for="character in characters" :key="character.id"
          >{{ character.name }},
        </span>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    image: String,
    description: String,
    date: String, // TODO: maybe change this to date
    creators: Array,
    characters: Array,
  },
  data() {
    return {
      fullView: false,
    };
  },
};
</script>

<style scoped></style>
