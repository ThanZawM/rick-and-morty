<template>
  <div class="details mt-10">
    <h1 class="my-16">Rick And Morty</h1>
    <v-row align="center">
      <v-col cols="6">
        <v-img class="details-image" :src="allData.image"> </v-img>
      </v-col>
      <v-col cols="6">
        <h2>{{ allData.name }}</h2>
        <h3>Status</h3>
        <v-card-title>{{ allData.status }}</v-card-title>
        <h3>Species</h3>
        <v-card-title>{{ allData.species }}</v-card-title>
        <h3>Gender</h3>
        <v-card-title>{{ allData.gender }}</v-card-title>
        <h3>Origin</h3>
        <v-card-title>{{ allData.origin.name }}</v-card-title>
        <h3>Last Known Location</h3>
        <v-card-title>{{ allData.location.name }}</v-card-title>
      </v-col>
    </v-row>
  </div>
</template>
  
  <script>
import axios from "axios";
export default {
  data() {
    return {
      allData: null,
      itemID: this.$route.params.id - 1,
    };
  },
  props: ["detailItem"],
  mounted() {
    // console.log("item id = " + this.itemID);
    this.getDataWithId();
  },
  methods: {
    getDataWithId() {
      axios
        .get("https://rickandmortyapi.com/api/character")
        .then((response) => {
          //   console.log(response.data.results);
          this.allData = response.data.results[this.itemID];
          console.log(this.allData);
        })
        .catch((error) => {
          alert(error);
        });
    },
  },
};
</script>

<style scoped>
.details-image {
  box-shadow: 0 10px 50px #66ba4f;
  border: 5px solid #272133;
  border-radius: 20px;
  margin-top: 20px;
  width: 60%;
  margin: auto;
}
</style>
  