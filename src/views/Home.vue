<template>
  <div class="animated fadeIn">
      <v-container>
        <v-row  >
          <v-col v-if="reveal" cols="12" md="12" sm="12">
            <Alert />
          </v-col>
          <v-col cols="12" md="12" sm="12">
            <Search @git="getList" @reveal="getError" />
          </v-col>
        </v-row>
        <v-row>
          <v-col md="3" v-for="card in cards" :key="card.name">
            <Cards
              :login="card.login"
              :id="card.id"
              :avatar_url="card.avatar_url"
              :html_url="card.html_url"
            />
          </v-col>
        </v-row>
      </v-container>
  </div>
</template>
<script>
import Cards from "../components/Cards";
import Search from "../components/Search";
import Alert from "../components/Alert";
export default {
  name:"Home",
  data: () => ({
    reveal: false,
    cards: null
  }),
  components: {
    Cards,
    Search,
    Alert
  },
  methods: {
    getList(data) {
      this.cards = data;
    },
    getError(data) {
      this.reveal = data;
       console.log(this.reveal)
      setTimeout(() => {
        this.reveal = false;
      }, 2000);
    },
  },
};
</script>
