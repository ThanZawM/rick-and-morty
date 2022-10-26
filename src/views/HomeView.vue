<template>
  <div class="home mt-10">
    <h1  class="mt-5 mb-10 header">Rick And Morty</h1>

    <!-- <SearchVue /> -->
    <!-- For search container -->
    <div class="search-container">
      <h2 class="search-title">Are you looking for a character?</h2>
      <v-form>
        <v-container>
          <v-row align="center" justify="center">
            <v-col cols="6" class="d-flex">
              <v-text-field
                solo
                placeholder="Write your name"
                v-model="inputName"
                @keyup.enter="filterSearch(inputName)"
              ></v-text-field>
              <v-btn icon>
                <v-icon color="orange" @click="filterSearch(inputName)">{{
                  mdiMagnify
                }}</v-icon>
              </v-btn>
            </v-col>
            <v-col cols="12" v-if="showClear">
              <v-btn color="#243e54" class="white--text text-uppercase mb-5" x-large dark outlined @click="clearSearch">clear search</v-btn>
            </v-col>
          </v-row>
        </v-container>
      </v-form>
    </div>

    <div class="card-container">
      <v-row align="center" no-gutters>
        <v-col cols="3" v-for="item in allData" :key="item.id">
          <router-link :to="{ name: 'details', params: { id: item.id } }">
            <HomeCard :obj="item" />
          </router-link>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HomeCard from "@/components/HomeCard.vue";
import axios from "axios";
import { mdiAccount, mdiMagnify } from "@mdi/js";

export default {
  name: "HomeView",
  components: { HomeCard },
  data: () => ({
    allData: null,
    mdiAccount: mdiAccount,
    mdiMagnify: mdiMagnify,
    showClear: false,
    inputName: "",
  }),
  mounted() {
    this.getData();
  },
  methods: {
    getData() {
      axios
        .get("https://rickandmortyapi.com/api/character")
        .then((response) => {
          this.allData = response.data.results;

          // console.log(this.allData);
        })
        .catch((error) => {
          alert(error);
        });
    },

    filterSearch(input) {
      this.showClear = true;

      var filter = this.allData.filter((el) =>
        el.name.toLowerCase().includes(input.toLowerCase())
      );
      console.log(filter);
      this.allData = filter;
    },

    clearSearch() {
      this.inputName = ''
      this.getData()
      this.showClear = false
    }
  },
};
</script>

<style scoped>
.header{
  font-size: 80px;
  font-weight: 400;
    color:#02b1c8;
    text-align: center;
    text-shadow: 1px 1px 1px #111;
    font-family: "Schoolbell",serif;
}
.search-title{
  font-size: 22px;
    font-weight: 900;
    text-align: center;
    color: #fff765;
    margin-bottom: 15px;
}
.v-btn:hover{
  background: #00b4cc;
}
</style>
