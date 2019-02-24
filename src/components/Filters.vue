<template>
    <v-btn color="success" v-on:click="changeSelectedCity">Success</v-btn>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Filters',
  components: {
  },
  props: {
  },
  data () {
    return {
    }
  },
  methods: {
    changeSelectedCity: function(){
      this.$emit('changeSelectedCity', 'chicago')
    },

    getAvaliableCities: function(){
      let url = `${process.env.VUE_APP_API_URL}markets/?format=json`
      this.isLoading = true
    }
  },
  created() {
  }
}
</script>

<style>
</style>
