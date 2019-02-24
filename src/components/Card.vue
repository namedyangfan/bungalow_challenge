<template>
  <v-container>
    <v-layout>
        <v-container grid-list-xl fluid px-0>
          <v-layout row wrap>
            <v-flex v-bind:key="bungalow.id" v-for="bungalow in bungalows" xs12 sm6 lg4 pa-1>
              <v-card flat tile>
                <v-img :src="bungalow.images[0].sm_url" aspect-ratio="1" />
              </v-card>
            </v-flex>
          </v-layout>
        </v-container>
    </v-layout>
  </v-container>
</template>

<script>
  
  export default {
    name: "Card",
    components: {
    },
    props: ["bungalows"]
  }
</script>

<style>

</style>
