<template>
  <div>
    <v-card color="#222831" class="rounded-lg pa-10 mx-6 mb-6 white--text" align="center" height="500">
      <v-img
        :src="obj.image"
        width="225"
        height="225"
        class="rounded-circle"
      ></v-img>
      <v-card-title>{{ obj.name }}</v-card-title>
      <v-card-title>
        <v-icon v-if="obj.status == 'Alive'" small color="green">{{ mdiCircle }}</v-icon>
          <v-icon v-else-if="obj.status == 'Dead'" small color="red">{{ mdiCircle }}</v-icon>
          <v-icon v-else small color="grey">{{ mdiCircle }}</v-icon>
          &nbsp;
        {{ obj.status }} - {{ obj.species }}
      </v-card-title>
      <v-card-actions>
        <v-btn x-large class="mt-4" dark outlined>See details</v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
import {mdiCircle} from '@mdi/js'
export default {
  data:() => ({
    mdiCircle: mdiCircle,
  }),
  props: ["obj"],
};
</script>

<style scoped>

.v-card__title, .v-card__actions{
    justify-content: center;
}
.v-btn:hover{
  color: #fff765;
}
</style>
