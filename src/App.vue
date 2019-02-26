<template>
  <v-app>
    <Filters 
      @changeSelectedCity   = "changeSelectedCity" 
      :filterAvaliableRooms = "filterAvaliableRooms"
      :selectedCity         = "selectedCity"
      :needClearFilter      = "needClearFilter"
      :updateFilterStatus   = "updateFilterStatus"
      :isLoading            = "isLoading"
      />
    <template v-if="isLoading ">
      <LoadingState />
    </template>
    <template v-else-if="isbungalowsListEmpty">
      <v-container fill-height>
        <div class="text-xs-center center-loading">
          <v-btn flat medium 
            @click='updateFilterStatus()'>
            Clear Filter
          </v-btn>
        </div>
      </v-container>
    </template>
    <template v-else>
      <v-content pt-60>
          <Card v-bind:bungalows="bungalows"/>
      </v-content>
    </template>
  </v-app>
</template>

<script>
import axios from 'axios'
import _     from 'lodash'

import Card     from './components/Card'
import Filters  from './components/Filters'
import LoadingState  from './components/LoadingState'

export default {
  name: 'App',
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
      selectedCity     : 'seattle',
      isLoading        : true,
      needClearFilter  : false
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

    updateFilterStatus: function(){
      this.bungalows = {...this.bungalowsCopy}
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
  }
</style>
