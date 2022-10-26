<template>
  <div>
    <v-card class="rounded-lg pa-10 mx-6 mb-6" align="center">
      <v-img
        :src="obj.image"
        width="225"
        height="225"
        class="rounded-circle"
      ></v-img>
      <v-card-title>{{ obj.name }}</v-card-title>
      <v-card-title>{{ obj.status }} - {{ obj.species }}</v-card-title>
      <v-card-actions>
        <v-btn class="mt-4" dark>See details</v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  props: ["obj"],
};
</script>

<style scoped>

.v-card__title, .v-card__actions{
    justify-content: center;
}
</style>
