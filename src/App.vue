<template>
  <v-app>
    <Filters @changeSelectedCity="changeSelectedCity" :selectedCity="selectedCity"/>
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
import axios    from 'axios'
import Card     from './components/Card'
import Filters  from './components/Filters'

export default {
  name: 'App',
  components: {
    Card,
    Filters
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
      let url = `${process.env.VUE_APP_API_URL}listings/properties/?market__slug=${this.selectedCity}`
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

    changeSelectedCity: function(city) {
      this.selectedCity = city
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
