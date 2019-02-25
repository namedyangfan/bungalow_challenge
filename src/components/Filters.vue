<template>
  <v-toolbar :light="true" :fixed="true" app flat>
  <v-container mx-auto py-0>
    <v-layout>
      <v-flex xs12 sm6 d-flex>
        <v-select 
          :label="selectedCityStyled"
          :items="avaliableCitiesList"
          solo
          prepend-inner-icon="search"
          color="success"
          @change="changeSelectedCity"
        ></v-select>
      </v-flex>
    </v-layout>
  </v-container>
</v-toolbar>
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

<style scoped>
  .v-input {
    font-weight: 800 !important;
    font-size: 17px !important;
  }
</style>
