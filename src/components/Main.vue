<template>
  <div class="main">
    <div>
      <Input @input="handleInput" />
      <b-list-group v-if="currentView == 'listView'" class="px-5">
        <!-- Create Character components for every character in results array, pass in data to props -->
        <div v-for="character in info" :key="character.id">
          <div class="row">
            <div class="col">
              <Character
                :name="character.name"
                :description="character.description"
                :thumbnail="
                  character.thumbnail.path + '.' + character.thumbnail.extension
                "
              />
            </div>
            <div class="col col-lg-1">
              <b-button
                @click="
                  (currentView = 'profileView'),
                    (selectedCharId = character.id),
                    (selectedCharName = character.name),
                    (selectedCharPic =
                      character.thumbnail.path +
                      '.' +
                      character.thumbnail.extension)
                "
                class="d-flex bg-dark text-warning"
                variant="outline"
                bg-variant="dark"
                size="lg"
                >Profile</b-button
              >
            </div>
          </div>
        </div>
      </b-list-group>
      <Profile
        v-if="currentView == 'profileView'"
        :characterId="selectedCharId"
        :Name="selectedCharName"
        :Pic="selectedCharPic"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import _ from "lodash";
import Character from "@/components/Character.vue";
import Profile from "@/components/Profile.vue";
import Input from "@/components/Input.vue";

export default {
  name: "Home",
  components: {
    Character,
    Input,
    Profile,
  },
  data() {
    return {
      info: null,
      publicKey: "4327819a4e9ae453434bb3d2dcc52456",
      time: 1564731162583,
      currentView: "listView", //default display- charList. can switch to profile view
      selectedCharId: "",
      selectedCharName: "",
      selectedCharPic: "",
    };
  },
  props: {
    searchName: String,
  },
  mounted() {
    this.getUrl(); // initial api request, will be updated by watcher function on searchName
  },
  methods: {
    getUrl() {
      if (this.Search) {
        axios
          .get(
            `https://gateway.marvel.com/v1/public/characters?&nameStartsWith=${
              this.Search
            }&ts=1&apikey=${
              this.publicKey
            }&hash=${"4dfd3313409d3a26b9513377ea1c2698".toLowerCase()}`
          )
          .then((response) => (this.info = response.data.data.results));
      } else {
        axios
          .get(
            `https://gateway.marvel.com/v1/public/characters?&ts=1&apikey=${
              this.publicKey
            }&hash=${"4dfd3313409d3a26b9513377ea1c2698".toLowerCase()}` //store this hashcode in a variable later please
          )
          .then((response) => (this.info = response.data.data.results));
      }
    },
    handleInput(value) {
      this.handleSearch(value);
    },
    showDesc() {},
    handleSearch: _.debounce(function(term) {
      if (this.currentView === "listView") {
        // actually remove this keep updating list if user types, and then if currentView isnt charList set it to that
        if (term) {
          axios
            .get(
              `https://gateway.marvel.com/v1/public/characters?&nameStartsWith=${term}&ts=1&apikey=${
                this.publicKey
              }&hash=${"4dfd3313409d3a26b9513377ea1c2698".toLowerCase()}`
            )
            .then((response) => (this.info = response.data.data.results));
        } else {
          axios
            .get(
              `https://gateway.marvel.com/v1/public/characters?&ts=1&apikey=${
                this.publicKey
              }&hash=${"4dfd3313409d3a26b9513377ea1c2698".toLowerCase()}`
            )
            .then((response) => (this.info = response.data.data.results));
        }
      } else {
        this.currentView = "listView";
      }
    }, 800),
  },

  watch: {
    // When searchName is changed update list of characters live

    searchName: function() {},
  },

  computed: {
    //get rid of this function
    Search() {
      return this.searchName;
    },
  },
};
</script>
