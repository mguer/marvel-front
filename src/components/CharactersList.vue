<template>
  <v-row class="justify-center">
    <v-card
      v-for="(character, index) in characters"
      :key="character.id+character.name"
      col="3"
      class="ma-5"
      max-width="344"
    >
      <v-img
        :src="character.thumbnail.path ? `${character.thumbnail.path}/${imgSize}` : defaultImg"
        class="white--text align-end"
        gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
        height="200px"
      >
        <v-card-title>{{ character.name }}</v-card-title>
      </v-img>

      <v-card-actions>
        <v-btn text>
          <v-icon>fas fa-heart</v-icon>
        </v-btn>

        <v-spacer></v-spacer>

        <v-btn
          icon
          @click="showInfo(index)"
        >
          <v-icon>fas fa-heart</v-icon>
        </v-btn>
      </v-card-actions>

      <v-expand-transition>
        <div v-show="index === selectedIndex ">
          <v-divider></v-divider>

          <v-card-text>
            I'm a thing. But, like most politicians, he promised more than he
            could deliver. You won't have time for sleeping, soldier, not with
            all the bed making you'll be doing. Then we'll go with that data
            file! Hey, you add a one and two zeros to that or we walk! You're
            going to do his laundry? I've got to find a way to escape.
          </v-card-text>
        </div>
      </v-expand-transition>
    </v-card>
  </v-row>
</template>

<script>
import axios from "axios";

export default {
  name: "CharactersList",
  data: () => ({
    url: "http://gateway.marvel.com/v1/public/characters",
    offset: "?offset=100",
    ts: "?ts=1519211809934",
    publicKey: "&apikey=a9d50df97a5f822a7edcd9afbe4e357a",
    hash: "&hash=a8add32b487ad7a6951689990256b007",
    imgSize: "standard_large.jpg",
    characters: [],
    selectedIndex : null,
    selectedHeroes: [],
    defaultImg:
      "https://blog.comic-con-paris.com/wp-content/uploads/2019/07/super-heros-marvel-min.jpg",
  }),
  methods: {
    async fetchData() {
      await axios
        .get(this.url + this.ts + this.publicKey + this.hash)
        .then((response) => {
          this.characters = response.data.data.results;
          response.data.data.results.forEach((item) => {
            this.characters.push(item);
          });
        });
      console.log(this.characters)
    },
    showInfo(index){
    console.log(this.selectedIndex)
    console.log(index)
    }
  },
  created() {
    this.fetchData();

  },
};
</script>

<style scoped></style>
