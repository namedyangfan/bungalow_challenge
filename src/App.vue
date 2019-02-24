<template>
  <v-app>
    <v-content>
      <Card v-bind:bungalows="bungalows"/>
    </v-content>
  </v-app>
</template>

<script>
import Card from './components/Card'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Card
  },
  data () {
    return {
      bungalows: [],
      errors  : []
    }
  },
  created() {
    axios.get(`https://fieldstone.bungalow.com/api/v1/listings/properties/?market__slug=seattle`)
    .then(response => {
      // JSON responses are automatically parsed.
      this.bungalows = response.data.results
      console.log(this.bungalows)
    })
    .catch(e => {
      this.errors.push(e)
      console.log(this.errors)
    })
  }
}
</script>
