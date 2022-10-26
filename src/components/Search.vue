<template>
  <div class="search-container">
    <h2>Are you looking for a character?</h2>
    <v-form>
      <v-container>
        <v-row align="center" justify="center">
          <v-col cols="6" class="d-flex">
            <v-text-field solo placeholder="Write your name"></v-text-field>
            <v-btn icon>
              <v-icon
                color="orange"
                @click="clickSearchBtn = !clickSearchBtn"
                >{{ mdiMagnify }}</v-icon
              >
            </v-btn>
          </v-col>
          <v-col cols="12" v-if="clickSearchBtn">
            <v-btn class="text-uppercase" dark>clear search</v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-form>
  </div>
</template>

<script>
import { mdiAccount, mdiMagnify } from "@mdi/js";
export default {
  name: "SearchVue",
  data: () => ({
    mdiAccount: mdiAccount,
    mdiMagnify: mdiMagnify,
    clickSearchBtn: false,
  }),
  name: "SearchVue",
  methods: {},
};
</script>

<style scoped>
</style>
