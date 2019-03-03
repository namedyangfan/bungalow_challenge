<template>
  <div>
    <Filters 
      @changeSelectedCity   = "changeSelectedCity" 
      :filterAvaliableRooms = "filterAvaliableRooms"
      :selectedCity         = "selectedCity"
      :needClearFilter      = "needClearFilter"
      :isLoading            = "isLoading"
      />
    <template v-if="isLoading ">
      <LoadingState />
    </template>
    <template v-else-if="isbungalowsListEmpty">
      <v-container fill-height>
        <v-layout row wrap align-center class="center-loading">
          <v-btn flat medium 
            @click='resetFilterStatus()'>
            Clear Filter
          </v-btn>
        </v-layout>
      </v-container>
    </template>
    <template v-else>
      <v-content pt-60>
          <Card v-bind:bungalows="bungalows"/>
      </v-content>
    </template>
  </div>
</template>

<script>
import axios from 'axios'
import _     from 'lodash'

import Card          from '@/components/Card'
import Filters       from '@/components/Filters'
import LoadingState  from '@/components/LoadingState'

export default {
  name: 'HomePage',
  components: {
    Card,
    Filters,
    LoadingState
  },
  data () {
    return {
      bungalows        : [],
      bungalowsCopy    : [],
      errors           : [],
      selectedCity     : this.$route.params.market_slug || 'seattle',
      isLoading        : null,
      needClearFilter  : false //a flag for reset filters
    }
  },
  methods: {
    getBungalows: function(){
      let url = `${process.env.VUE_APP_API_URL}listings/properties/?market__slug=${this.selectedCity}`
      this.isLoading = true

      axios.get(url)
      .then(response => {
        this.bungalows     = response.data.results
        this.bungalowsCopy = response.data.results
        this.isLoading     = false
      })
      .catch(e => {
        this.errors.push(e)
        this.isLoading = false
      })
    },

    changeSelectedCity: function(city) {
      this.selectedCity = city
      this.getBungalows()
    },

    filterAvaliableRooms: function(avaliableRoomRange){
      this.bungalows = _.filter(this.bungalowsCopy, function(bungalow) { 
        return bungalow.available_room_count>=avaliableRoomRange[0] && 
          bungalow.available_room_count<=avaliableRoomRange[1]; 
      });
    },

    resetFilterStatus: function(){
      this.bungalows       = [...this.bungalowsCopy]

      this.needClearFilter = !this.needClearFilter
    }
  },
  created() {
    this.getBungalows()
  },
  computed: {
   isbungalowsListEmpty: function (){
      return _.isEmpty(this.bungalows)
    }
  }
}
</script>

<style>
  .center-loading{
    padding-left: 45%;
    padding-top: 20%;
  }
</style>
