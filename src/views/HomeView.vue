<template>
  <div class="home mt-10">
    <h1 class="mt-5 mb-10 header">Rick And Morty</h1>

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
                @keyup.enter="filterSearch(inputName, false)"
              ></v-text-field>
              <v-btn icon>
                <v-icon
                  color="orange"
                  @click="filterSearch(inputName, false)"
                  >{{ mdiMagnify }}</v-icon
                >
              </v-btn>
            </v-col>
            <v-col cols="12" v-if="showClear">
              <v-btn
                color="#243e54"
                class="white--text text-uppercase mb-5"
                x-large
                dark
                outlined
                @click="clearSearch"
              >
                clear search</v-btn
              >
            </v-col>
          </v-row>
        </v-container>
      </v-form>
    </div>

    <div class="card-container">
      <v-row align="center" no-gutters>
        <v-col
          cols="12"
          lg="3"
          md="4"
          sm="6"
          v-for="item in allData"
          :key="item.id"
        >
          <HomeCard :obj="item" />
        </v-col>
      </v-row>
    </div>

    <div class="text-center">
      <v-pagination
        v-model="currPage"
        :length="totalPages"
        circle
        :total-visible="7"
        :value="currPage"
        :prev-icon="mdiChevronDoubleLeft"
        :next-icon="mdiChevronDoubleRight"
      ></v-pagination>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HomeCard from "@/components/HomeCard.vue";
import axios from "axios";
import {
  mdiMagnify,
  mdiChevronDoubleLeft,
  mdiChevronDoubleRight,
} from "@mdi/js";

export default {
  name: "HomeView",
  components: { HomeCard },
  data: () => ({
    allData: null,
    searchData: null,
    mdiMagnify: mdiMagnify,
    showClear: false,
    inputName: "",
    currPage: 1,
    totalPages: 42,
    mdiChevronDoubleLeft: mdiChevronDoubleLeft,
    mdiChevronDoubleRight: mdiChevronDoubleRight,
  }),
  mounted() {
    let self = this;
    self.getData(self.currPage);
  },
  watch: {
    currPage() {
      let self = this;
      if (self.inputName) {
        self.filterSearch(self.inputName, true);
      } else {
        self.getData(self.currPage);
      }
    },
  },
  // updated() {
  //   let self = this;
  //   self.getData(self.currPage);
  // },
  methods: {
    getData(pageNO) {
      let self = this;
      axios
        .get("https://rickandmortyapi.com/api/character?page=" + pageNO)
        .then((response) => {
          self.allData = response.data.results;
          self.totalPages = response.data.info.pages;
        })
        .catch((error) => {
          alert(error);
        });
    },

    filterSearch(input, isPagination) {
      let self = this;
      self.showClear = true;
      if (!isPagination) self.currPage = 1;
      axios
        .get(
          "https://rickandmortyapi.com/api/character?page=" +
            self.currPage +
            "&name=" +
            input
        )
        .then((response) => {
          self.allData = response.data.results;
          self.totalPages = response.data.info.pages;
        })
        .catch((error) => {
          alert(error);
        });

      // let filter = self.allData.filter((el) =>
      //   el.name.toLowerCase().includes(input.toLowerCase())
      // );
      // self.allData = filter;
    },

    clearSearch() {
      let self = this;
      self.inputName = "";
      self.getData(self.currPage);
      self.showClear = false;
    },
  },
};
</script>

<style scoped>
.header {
  font-size: 80px;
  font-weight: 400;
  color: #02b1c8;
  text-align: center;
  text-shadow: 1px 1px 1px #111;
  font-family: "Schoolbell", serif;
}

.search-title {
  font-size: 22px;
  font-weight: 900;
  text-align: center;
  color: #fff765;
  margin-bottom: 15px;
}

.v-btn:hover {
  background: #00b4cc;
}
</style>
