<template>
  <v-app>
    <Navbar />
    <v-main>
      <keep-alive include="Home">
      <router-view />
      </keep-alive>
    </v-main>
  </v-app>
</template>

<script>
import Navbar from "../src/components/NavBar"
export default {
  name: "App",
  
   components: {
      Navbar
    },
};
</script>
