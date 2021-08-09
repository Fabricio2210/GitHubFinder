<template>
  <v-container>
    <Spinner v-if="isLoading" class="pa-6" />
    <div v-if="!isLoading" >
      <v-form v-model="valid">
        <v-text-field
          v-model="text"
          label="Type something..."
          required
        ></v-text-field>
      </v-form>
      <v-btn block class="white--text" color="grey darken-3" @click="getForm()">
        Search
      </v-btn>
      <v-btn class="mt-3" color="grey lighten-4 " block @click="clearForm()">
        Clear
      </v-btn>
    </div>
  </v-container>
</template>
<script>
import axios from "axios";
import Spinner from "./Spinner";
export default {
  data: () => ({
    text: "",
    valid: true,
    data: null,
    reveal: false,
    isLoading: false,
  }),
  components: {
    Spinner,
  },
  methods: {
    async getForm() {
      if (this.text == "") {
        this.reveal = true;
        this.$emit("reveal", this.reveal);
      } else {
        this.isLoading = true;
        const res = await axios.get(
          `https://api.github.com/search/users?q=${this.text}`
        );
        this.isLoading = false;
        this.data = res.data.items;
        this.$emit("git", this.data, this.reveal);
      }
    },
    clearForm() {
      this.text = "";
      this.data = "";
      this.$emit("git", this.data);
    },
  },
};
</script>
