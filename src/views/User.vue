<template>
  <v-container class="animated fadeIn">
    <Spinner v-if="isLoading" />
    <v-card class="pa-5">
      <div class="d-sm-flex d-md-none">
        <v-row>
          <v-col align="center">
            <v-avatar size="120px" class="pa-1">
              <v-img :src="infoUser.avatar_url"></v-img>
            </v-avatar>
            <h3 class="text-center pa-2">{{ infoUser.login }}</h3>
            <p v-if="hasBio" class="text-center pa-1">
              <span class="font-weight-bold">Bio:</span> {{ infoUser.bio }}
            </p>
            <p>
              <span class="font-weight-bold">Location:</span>
              {{ infoUser.location }}
            </p>
             <p> <v-btn class="me-2" :href="infoUser.html_url" elevation="2" rounded>GitHub</v-btn></p>
            <v-btn depressed>
              <v-icon left dark>
                mdi-arrow-left-bold
              </v-icon>
              <router-link tag="button" to="/">Back</router-link>
            </v-btn>
          </v-col>
        </v-row>
      </div>
      <div class="d-none d-md-flex d-lg-flex ">
        <v-row>
          <v-col md="1">
            <v-avatar size="120px" class="pa-1">
              <v-img :src="infoUser.avatar_url"></v-img>
            </v-avatar>
          </v-col>
          <v-col>
            <v-card-title>{{ infoUser.login }}</v-card-title>
            <v-card-text>
              <p v-if="hasBio">
                <span class="font-weight-bold">Bio:</span> {{ infoUser.bio }}
              </p>
              <p>
                <span class="font-weight-bold">Location:</span>
                {{ infoUser.location }}
              </p>
              <p>
                <v-btn class="me-2" :href="infoUser.html_url" elevation="2" rounded>GitHub Page</v-btn>
              </p>
            </v-card-text>
            <v-btn depressed>
              <v-icon left dark>
                mdi-arrow-left-bold
              </v-icon>
              <router-link tag="button" to="/">Back</router-link>
            </v-btn>
          </v-col>
        </v-row>
      </div>
    </v-card>
  </v-container>
</template>
<script>
import axios from "axios";
import Spinner from "../components/Spinner";
export default {
  data: () => ({
    infoUser: null,
    hasBio: true,
    isLoading: false,
  }),
  components: {
    Spinner,
  },
  methods: {
    async getUser() {
      this.isLoading = true;
      const res = await axios.get(
        `https://api.github.com/users/${this.$route.params.id.login}`
      );
      this.isLoading = false;
      this.infoUser = res.data;
      console.log(this.infoUser);
      if (this.infoUser.bio === null) {
        this.hasBio = false;
      }
    },
  },
  mounted() {
    this.getUser();
  },
};
</script>
