<template>
  <v-app>
    <v-app-bar app color="error" dark>

      <v-spacer></v-spacer>

      <v-btn
        text
      >
        <span class="mr-2">Marvel test</span>

      </v-btn>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>
