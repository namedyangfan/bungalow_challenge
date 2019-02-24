<template>
  <v-container>
    <v-layout>
        <v-container grid-list-xl fluid px-0>
          <v-layout row wrap>
            <v-flex v-bind:key="bungalow.id" v-for="bungalow in bungalows" xs12 sm6 lg4 pa-1>
              <v-card flat tile>
                <v-img :src="bungalow.images[0].sm_url" aspect-ratio="1" />
                <CardDescription v-bind:bungalowHeadline="bungalow.headline" v-bind:headline="bungalow.headline"
                  v-bind:available_room_count="bungalow.available_room_count" 
                  v-bind:total_room_count="bungalow.total_room_count"
                  v-bind:room_prices="bungalow.room_prices"
                  v-bind:earliest_available_date="bungalow.earliest_available_date"/>
              </v-card>
            </v-flex>
          </v-layout>
        </v-container>
    </v-layout>
  </v-container>
</template>

<script>
  import CardDescription from './CardDescription'
  
  export default {
    name: "Card",
    components: {
      CardDescription
    },
    props: ["bungalows"]
  }
</script>

<style>

</style>
