<template>
  <v-container fluid grid-list-xl>
    <v-layout wrap>
      <v-flex xs12 sm6 d-flex>
        <v-select
          :label="selectedCityStyled"
          :items="avaliableCitiesList"
          item-value="initialv"
          solo
          prepend-inner-icon="search"
          @change="changeSelectedCity"
        ></v-select>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import axios from 'axios'
import _     from 'lodash'

export default {
  name: 'Filters',

  props: {
    selectedCity : String
  },

  data () {
    return {
      avaliableCitiesList : [],
      avaliableCities     : null,
      errors              : [],
    }
  },

  created() {
    this.getAvaliableCities()
  },

  methods: {

    changeSelectedCity: function(city){
      let cityValidate = city.replace(/\s+/g, '-').toLowerCase()
      this.$emit('changeSelectedCity', cityValidate)
    },

    getAvaliableCities: function(){
      let url = `${process.env.VUE_APP_API_URL}markets/?format=json`

      axios.get(url)
      .then(response => {
        this.avaliableCities = response.data.results
        this.avaliableCitiesList = this.avaliableCities.map(city => city.internal_name)
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
</style>
