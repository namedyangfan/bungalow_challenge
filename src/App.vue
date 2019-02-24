<template>
  <v-app>
    <v-btn color="success" v-on:click="changeSelectedCity('chicago')">Success</v-btn>
    <template v-if="isLoading ">
      <v-container  fill-height>
        <div class="text-xs-center center-loading">
          <v-progress-circular :size="100" color="primary" indeterminate>
          </v-progress-circular>
        </div>
    </v-container>
    </template>
    <template v-else>
      <v-content>
        <Card v-bind:bungalows="bungalows"/>
      </v-content>
    </template>
  </v-app>
</template>

<script>
import Card  from './components/Card'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Card
  },
  data () {
    return {
      bungalows    : [],
      errors       : [],
      selectedCity : 'seattle',
      isLoading    : true
    }
  },
  methods: {
    getBungalows: function(){
      
      let url = `https://fieldstone.bungalow.com/api/v1/listings/properties/?market__slug=${this.selectedCity}`
      this.isLoading = true

      axios.get(url)
      .then(response => {
        this.bungalows = response.data.results
        this.isLoading = false
        console.log(this.bungalows)
      })
      .catch(e => {
        this.errors.push(e)
        this.isLoading = false
        console.log(this.errors)
      })
    },

    changeSelectedCity: function(e) {
      this.selectedCity = e
      this.getBungalows()
    }
  },
  created() {
    this.getBungalows()
  }
}
</script>

<style>
  .center-loading{
    padding-left: 45%;
  }
</style>
