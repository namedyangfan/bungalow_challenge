<template>
  <v-container>
    <v-layout>
        <v-container grid-list-xl fluid px-0>
          <v-layout row wrap>
              <v-flex v-bind:key="bungalow.id" v-for="bungalow in bungalows" xs12 sm6 lg4 pa-1>
                <v-hover>
                  <v-card flat tile slot-scope="{ hover }">
                      <v-carousel hide-delimiters :cycle="false" :hide-controls="hover ? false : true">
                        <v-carousel-item
                          v-for="(image,i) in bungalow.images"
                          :key="i"
                          :src="image.sm_url"
                        ></v-carousel-item>
                      </v-carousel>
                    <CardDescription v-bind:bungalowHeadline="bungalow.headline" v-bind:headline="bungalow.headline"
                      v-bind:available_room_count="bungalow.available_room_count" 
                      v-bind:total_room_count="bungalow.total_room_count"
                      v-bind:room_prices="bungalow.room_prices"
                      v-bind:earliest_available_date="bungalow.earliest_available_date"/>
                  </v-card>
                </v-hover>
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
    data() {
      return {
        hover: false,
      };
    },
    props: ["bungalows"]
  }
</script>

<style>

</style>
