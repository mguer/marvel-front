<template>
  <div class="col-12">
    <v-card v-for="character in characters" :key="character.id" >
      <v-img
        :src="dd"
        class="white--text align-end"
        gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
        height="200px"
      >
        <v-card-title :v-text="character.name"></v-card-title>
      </v-img>

      <v-card-actions>
        <v-spacer></v-spacer>

        <v-btn icon>
          <v-icon>fas fa-heart</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-bookmark</v-icon>
        </v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "CharactersList",
  data: () => ({
    url: "http://gateway.marvel.com/v1/public/characters?",
    ts: "ts=1519211809934",
    publicKey: "&apikey=a9d50df97a5f822a7edcd9afbe4e357a",
    hash: "&hash=a8add32b487ad7a6951689990256b007",
    characters: [],
  }),
  async created() {
    await axios
      .get(
        this.url + this.ts + this.publicKey + this.hash
      )
      .then((response) => {
        this.characters = response.data;
      });
    console.log(this.url + this.ts + this.publicKey + this.hash);
    console.log(this.characters.data);
  },
};
</script>

<style scoped></style>
