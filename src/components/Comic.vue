<template>
  <div @click="fullView = !fullView">
    <!-- These comics should just be converted into the bootstrap card class? -->
    <div class=" mx-auto">
      <img :src="image" class="img-fluid" />
    </div>
    <!-- When Comic is clicked, fullview is turned on or off // I want this to open up to the side of the comic -->
    <div v-if="fullView" class="bg-dark text-light">
      <p class="lead font-italic">{{ title }}</p>
      <p>{{ description }}</p>
      <ul>
        Created by:
        <span v-for="creator in creators" :key="creator.id" class="text-left">
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
