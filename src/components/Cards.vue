<template>
  <div>
    <v-card class="mx-auto pa-4" max-width="344">
      <v-row>
        <v-col md="3" sm="2" xs="1">
          <v-avatar size="96px" class="pa-1">
            <v-img :src="avatar_url"></v-img>
          </v-avatar>
        </v-col>
        <v-col class="text-center">
          <v-card-text>
            <p class="subtitle-1 text--primary">
              {{ login }}
            </p>
            <v-btn depressed  @click="getUser()">
              <router-link tag="button" :to="{name :'User', params:{id:{login}}}">More</router-link>
            </v-btn>
          </v-card-text>
        </v-col>
      </v-row>
      <!-- <v-card-actions>
        <v-btn text color="teal accent-4" @click="reveal = true">
          Learn More
        </v-btn>
      </v-card-actions> -->
    </v-card>
  </div>
</template>
<script>
import axios from "axios"
export default {
  props: ["login", "id", "avatar_url","html_url"],
  methods:{
    async getUser(){
       const res = await axios.get(`https://api.github.com/search/users/${this.login}`)
       console.log(res.data)
    }
  }
};
</script>
