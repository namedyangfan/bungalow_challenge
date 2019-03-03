<template>
  <v-toolbar :light="true" :fixed="true" app flat>
  <v-container mx-auto py-0>
    <v-layout row wrap>
      <v-flex xs12 sm1 md1 d-flex>
        <v-img
            :src       = "require('.././assets/logo.png')"
            class      = "mr-5"
            min-width  = "50"
            max-height = "50"
            contain
        />
      </v-flex>
      <v-flex xs6 sm5 md3 pt-1>
        <v-select 
          :label             = "selectedCityStyled"
          :items             = "avaliableCitiesObj"
          item-text          = "display_name"
          item-value         = "slug"
          prepend-inner-icon = "search"
          color              = "success"
          @change            = "changeSelectedCity"
          solo
          autocomplete 
          search-input.sync
        ></v-select>
      </v-flex>
      <v-flex xs2 sm5 md3 pt-1>
        <RoomFilter 
          :filterAvaliableRooms = "filterAvaliableRooms"
          :needClearFilter      = "needClearFilter"
          :isLoading            = "isLoading"
        />
      </v-flex>
    </v-layout>
  </v-container>
</v-toolbar>
</template>

<script>
import axios from 'axios'
import _     from 'lodash'

import RoomFilter from './RoomFilter'

export default {
  name: 'Filters',
  components: {
    RoomFilter
  },
  props: {
    selectedCity         : String,
    needClearFilter      : Boolean,
    isLoading            : Boolean,
    filterAvaliableRooms : Function
  },

  data () {
    return {
      avaliableCitiesObj  : [],
      errors              : [],
    }
  },

  created() {
    this.getAvaliableCities()
    this.updateRouterParams(this.selectedCity)
  },

  methods: {

    updateRouterParams: function(city){
      this.$router.replace({ 
        params: {market_slug: city},
        query: {...this.$route.query} 
      })
      console.log()
    },

    changeSelectedCity: function(city){
      this.$emit('changeSelectedCity', city)
      this.updateRouterParams(city)
    },

    getAvaliableCities: function(){
      let url = `${process.env.VUE_APP_API_URL}markets/?format=json`

      axios.get(url)
      .then(response => {
        this.avaliableCitiesObj = _.map(
          response.data.results, function(currentObject) {
            return _.pick(currentObject, "display_name", "slug");
        });
      })
      .catch(e => {
        this.errors.push(e)
      })
    }
  },

  computed: {
   selectedCityStyled: function (){
      return _.startCase(_.toLower(this.selectedCity))
    }
  }
}
</script>

<style>
  .theme--light.v-input:not(.v-input--is-disabled) input, 
    .theme--light.v-input:not(.v-input--is-disabled) textarea {
    font-weight: 800 !important;
    font-size: calc(12px + 0.5vw) !important;
    color: #424242;
  }

  .v-select__slot .v-label {
    font-size: calc(12px + 0.5vw) !important;
    font-weight: 800 !important;
    color: #424242;
}
</style>
