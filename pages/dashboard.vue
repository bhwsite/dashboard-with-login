<script>
import {
  mapActions
} from "vuex";
export default {
  async fetch(){
    this.users = await fetch(
      'https://jsonplaceholder.typicode.com/photos').then((res) => res.json())
  },
  data() {
    return {
      users: [],
      search: "",
      sliceNumber: 8,
    };
  },
  computed: {
    filteredUsers() {
      console.log("filter", this.users)
      return this.users.slice(0, this.sliceNumber).filter(obj => Object.values(obj).some(val => String(val).includes(this.search)))
    },
  },
  methods: {
    ...mapActions('data', ['getData']),
    
    darkMode() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    },
  },
};
</script>

<template>
  <div>
    <v-row>
      <v-col style="position: absolute; right: 0;">
        <v-footer>
          <v-col cols="1">
            <v-btn @click="darkMode">
              <v-icon class="mr-2">
                mdi-brightness-4
              </v-icon>
            </v-btn>
          </v-col>
          <v-col cols="2">
            <h1 class="author"> Altug Erdem</h1>
          </v-col>
          <v-col cols="6">
            <input
              v-if="this.$vuetify.theme.dark == false"
              class="input"
              type="text"
              v-model="search"
              placeholder="Search User Profiles"
            >
            <input
              v-if="this.$vuetify.theme.dark == true"
              class="inputDark"
              type="text"
              v-model="search"
              placeholder="Search User Profiles"
            >
          </v-col>
          <v-spacer></v-spacer>
          <v-col cols="2">
            <div style="position: flex; float: right;">
              <v-tabs>
                <v-tab to="dashboard">Page 1</v-tab>
                <v-tab to="cardView">Page 2</v-tab>
              </v-tabs>
            </div>
            <!-- <v-btn >Page 1</v-btn>
          <v-btn>Page 2</v-btn> -->
          </v-col>
        </v-footer>
      </v-col>
    </v-row>

    <v-row>
      <v-col
        style="display: flex; flex-wrap: wrap; justify-content: center; margin-top: 10%"
        cols="12"
      >
        <v-card
          class="cards"
          v-for="user in filteredUsers.slice(0,8)"
          :key="user.id"
        >
          <v-img :src="`${user.url}`">
          </v-img>
          <v-card-text>
            <div style="text-transform:capitalize;"> {{user.userId}}.{{user.title}} </div>
            <div>
              {{user.body}}
            </div>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<style>
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;

}

.cards {
  height: 325px;
  width: 230px;
  margin: 2%
}
.input {
  border-style: solid;
  border-color: black;
  width: 100%;
}
.wrapper {
  margin: 1%;
  padding: 1%;
}
.fetchButton {
  justify-content: center;
}
.inputDark{
  background-color: white;
  width: 100%;
}
.author{
  font-weight: bold; 
  margin: 0px auto;
  display: block; 
}
</style>
