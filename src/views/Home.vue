<template>
  <v-container>
  <characters-list />
  </v-container>
</template>

<script>
import CharactersList from "../components/CharactersList";

export default {
  name: "Home",

  components: {
    CharactersList,
  },
};
</script>
