<template>
  <v-row class="justify-center">
    <v-card col="3" class="ma-5" width="350">
      <v-card-title>Mes personnages préférés</v-card-title>
      <v-list-item>
        <v-list-item-content >
          <p v-for="(hero, index) in bookmarkHeroes" :key="hero+index">{{ hero }}</p>
        </v-list-item-content>
      </v-list-item>
    </v-card>

    <v-card
        v-for="(character, index) in characters"
        :key="character.id + character.name + index"
        col="3"
        class="ma-5"
        width="350"
    >
      <v-img
          :src="
          character.thumbnail.path
            ? `${character.thumbnail.path}/${imgSize}`
            : defaultImg
        "
          class="white--text align-end"
          gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
      >
        <v-card-title>{{ character.name }}</v-card-title>
      </v-img>

      <v-card-actions>
        <v-btn text @click="addToBookmark(character.name)">
          <v-icon>fas fa-heart</v-icon>
        </v-btn>

        <v-spacer></v-spacer>

        <v-btn icon @click="showInfo(index)">
          <v-icon>{{
              index === selectedIndex ? "fas fa-arrow-up" : "fas fa-arrow-down"
            }}</v-icon>
        </v-btn>
      </v-card-actions>

      <v-expand-transition>
        <div v-show="index === selectedIndex">
          <v-divider></v-divider>

          <v-card-text>
            {{
              character.description
                  ? character.description
                  : "pas de description"
            }}
          </v-card-text>
          <v-card-text>
            nombre de comics : {{ character.comics.items.length }}
          </v-card-text>
          <v-card-text
              v-for="(comics, index) in character.comics.items.slice(0, 3)"
              :key="comics.name"
          >
            {{ index + 1 }} : {{ comics.name }}
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
    //url params
    url: "http://gateway.marvel.com/v1/public/characters",
    limit: "?limit=20",
    offset: "&offset=100",
    ts: "&ts=1519211809934",
    publicKey: "&apikey=a9d50df97a5f822a7edcd9afbe4e357a",
    hash: "&hash=a8add32b487ad7a6951689990256b007",
    imgSize: "standard_large.jpg",
    //layouts options
    characters: [],
    selectedIndex: null,
    bookmarkHeroes: [],
    defaultImg:
        "https://blog.comic-con-paris.com/wp-content/uploads/2019/07/super-heros-marvel-min.jpg",
  }),
  methods: {
    async fetchData() {
      await axios
          .get(this.url + this.limit + this.offset + this.ts + this.publicKey + this.hash)
          .then((response) => {
            this.characters = response.data.data.results;
            response.data.data.results.forEach((item) => {
              this.characters.push(item);
              console.log(item);
            });
          });
      console.log(this.characters);
    },
    showInfo(index) {
      this.selectedIndex == index ? this.selectedIndex = null : this.selectedIndex = index ;
    },
    addToBookmark(hero) {
      if (!this.bookmarkHeroes.includes(hero)) {
        if (this.bookmarkHeroes.length > 4) {
          this.bookmarkHeroes.splice(0, 1);
        }
        this.bookmarkHeroes.push(hero);
      }
    },
  },
  created() {
    this.fetchData();
  },
};
</script>

<style scoped></style>
