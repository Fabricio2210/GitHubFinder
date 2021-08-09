<template>
  <v-app-bar app color="grey darken-4" dark>
    <div class="d-flex align-center">
      <v-toolbar-title>
        <v-icon large color="white">
          mdi-github
        </v-icon>
        GitHub Finder</v-toolbar-title
      >
    </div>
    <v-spacer></v-spacer>
    <v-btn text>
      <router-link class="white--text" to="/">Home</router-link>
    </v-btn>
    <v-btn class="ma-2" text>
      <router-link class="white--text" to="/about">About</router-link>
    </v-btn>
  </v-app-bar>
</template>
