<template>
  <v-toolbar :light="true" :fixed="true" app flat>
  <v-container mx-auto py-0>
    <v-layout>
      <v-flex sm1 md1 d-flex>
        <v-img
            :src="require('.././assets/logo.png')"
            class="mr-5"
            contain
            min-width="50"
            max-height="50"
        />
      </v-flex>
      <v-flex sm11 md3 d-flex pt-1>
        <v-select 
          :label="selectedCityStyled"
          :items="avaliableCitiesObj"
          item-text="display_name"
          item-value="slug"
          solo
          prepend-inner-icon="search"
          color="success"
          @change="changeSelectedCity"
          autocomplete 
          search-input.sync
        ></v-select>
      </v-flex>
      <RoomFilter :filterAvaliableRooms="filterAvaliableRooms"/>
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
  },

  methods: {

    changeSelectedCity: function(city){
      console.log(city)
      this.$emit('changeSelectedCity', city)
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
    font-size: 17px !important;
    color: #424242;
  }

  .v-select__slot .v-label {
    font-size: 17px !important;
    font-weight: 800 !important;
    color: #424242;
}
</style>
