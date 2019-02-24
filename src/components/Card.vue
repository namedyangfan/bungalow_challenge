<template>
  <v-container>
    <v-layout>
        <v-container grid-list-xl fluid px-0>
          <v-layout row wrap>
              <v-flex v-bind:key="bungalow.id" v-for="bungalow in bungalows" xs12 sm6 lg4 pa-1>
                <v-hover>
                  <v-card flat tile slot-scope="{ hover }" height="100%">
                      <v-carousel hide-delimiters :cycle="false" :hide-controls="hover ? false : true" :height="250" >
                        <v-carousel-item
                          v-for="(image,i) in bungalow.images"
                          :key    = "i"
                          :src    = "image.sm_url"
                          :srcset = "getSrcSet(image)"
                          :sizes  = "getSizes()"
                          :lazy   = "true"
                        ></v-carousel-item>
                      </v-carousel>
                    <CardDescription 
                      :bungalowHeadline="bungalow.headline" 
                      :headline="bungalow.headline"
                      :available_room_count="bungalow.available_room_count" 
                      :total_room_count="bungalow.total_room_count"
                      :room_prices="bungalow.room_prices"
                      :earliest_available_date="bungalow.earliest_available_date"/>
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
    props: {
      bungalows  : Array,
      cardHeight : Number,
    },
    data() {
      return {
        hover: false,
        height: null
      };
    },
    methods: {
      getSrcSet(image) {
        const srcset = `${image.lg_url} 1500w, ${image.md_url} 960w, ${image.sm_url} 560w`
        return srcset
      },

      getSizes() {
        const sizes = '(min-width: 1264px) 30vw, (min-width: 600px) 45vw, 98vw'
        // const sizes = "(min-width: 40em) calc(66.6vw - 4em), 100vw"
        return sizes
      },

      getCarouselHeight () {
        var item = document.getElementsByClassName('v-image__image--cover')
         this.carouselHeight = item[0].clientHeight + 'px'
      },
    }
  }
</script>

<style scoped>
.auto-height {
    height: auto !important;
}
</style>
