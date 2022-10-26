<template>
  <div class="details mt-10">
    <h1 class="header mt-5 mb-10">Rick And Morty</h1>
    <v-row align="center">
      <v-col cols="6">
        <v-img class="details-image" :src="allData.image"> </v-img>
      </v-col>
      <v-col cols="6">
        <h2>{{ allData.name }}</h2>
        <h3>Status:</h3>
        <v-card-title>
          <v-icon v-if="allData.status == 'Alive'" small color="green">{{ mdiCircle }}</v-icon>
          <v-icon v-else-if="allData.status == 'Dead'" small color="red">{{ mdiCircle }}</v-icon>
          <v-icon v-else small color="grey">{{ mdiCircle }}</v-icon>
          &nbsp;{{ allData.status }}
        </v-card-title>


        <v-row>
          <v-col cols="6">
            <h3>Species:</h3>
          </v-col>
          <v-col cols="6">
            <h3>Gender:</h3>
          </v-col>
          <v-col cols="6">
            <v-card-title>{{ allData.species }}</v-card-title>
          </v-col>
          <v-col cols="6">
            <v-card-title>{{ allData.gender }}</v-card-title>
          </v-col>
          <v-col cols="6">
            <h3>Origin:</h3>
          </v-col>
          <v-col cols="6">
            <h3>Last Known Location:</h3>
          </v-col>
          <v-col cols="6">
            <v-card-title>{{ allData.origin.name }}</v-card-title>
          </v-col>
          <v-col cols="6">
            <v-card-title>{{ allData.location.name }}</v-card-title>
          </v-col>
        </v-row>

        <v-btn outlined dark x-large class="text-uppercase mt-5" to="/">
          go to main menu
        </v-btn>
      </v-col>
    </v-row>
  </div>
</template>
  
<script>
import { mdiCircle } from '@mdi/js'
import axios from "axios";
export default {
  data() {
    return {
      allData: null,
      itemID: this.$route.params.id - 1,
      mdiCircle: mdiCircle,
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

h2 {
  font-size: 40px;
  letter-spacing: 2px;
  text-align: left;
  margin-bottom: 25px;
  color: white;
}

h3 {
  font-size: 24px;
  color: #a9a9a9;
  text-align: left;
  ;
}

.v-card__title:hover {
  color: #ffe593;
}
.v-card__title{
  color: white;
}
.header {
  color: #02b1c8;
  font-size: 80px;
  font-weight: 400;
    color:#02b1c8;
    text-align: center;
    text-shadow: 1px 1px 1px #111;
    font-family: "Schoolbell",serif;
}
.v-btn:hover{
  color: #fff765;
}
</style>
  