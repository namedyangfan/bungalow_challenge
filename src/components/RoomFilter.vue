<template>
  <v-menu offset-y content-class="filter-menu" light z-index="1000"
    :close-on-content-click="false" max-width="300" nudge-bottom="10" max-height="150">
    <v-btn
      slot="activator"
      class="text-capitalize white room-filter"
    >
      <span text-capitalize class="filter-menu-text">Avaliable Rooms</span>
    </v-btn>
    <v-flex pt-3 pl-4 pr-4>
      <v-range-slider
        v-on:change="updateFilterVarAvaliableRooms"
        v-model="avaliableRoomRange"
        :max="10"
        :min="1"
        always-dirty
        thumb-label="always"
        thumb-size="25"
      ></v-range-slider>
    </v-flex>
  </v-menu>
</template>

<script>
import _ from 'lodash'

export default {
  name: 'RoomFilter',
  props: {
    needClearFilter      : Boolean,
    isLoading            : Boolean,
    filterAvaliableRooms : Function
  },

  data () {
    return {
      avaliableRoomRange  : [1,10],
      filterMin           : this.$route.query.availableRoomsMin || 1,
      filterMax           : this.$route.query.availableRoomsMax || 10
    }
  },

  methods: {
    getFilterVariableFromQuery: function(){
      if(this.avaliableRoomRange[0]!=this.filterMin || this.avaliableRoomRange[1]!=this.filterMax){
        this.avaliableRoomRange = [this.filterMin, this.filterMax]
        this.filterAvaliableRooms(this.avaliableRoomRange)
      }
    },

    updateRouterParams: function(){
      this.$router.replace({ query: 
        { ...this.$route.query,
          availableRoomsMin: this.avaliableRoomRange[0],
          availableRoomsMax: this.avaliableRoomRange[1]} 
      })
    },

    debounceFilterAvaliableRooms:_.debounce(function() {
      this.filterAvaliableRooms(this.avaliableRoomRange)
    }, 500),

    updateFilterVarAvaliableRooms: function(){
      this.updateRouterParams()
      this.debounceFilterAvaliableRooms()
    },
  },

  created() {
    this.getFilterVariableFromQuery()
    this.updateRouterParams()
  },
  watch: {
    needClearFilter: function(){
      this.avaliableRoomRange = [1,10];
      this.updateRouterParams();
    },

    isLoading: function(){
      this.isLoading?(
        null
      ):(
        this.filterAvaliableRooms(this.avaliableRoomRange)
      )
    }
  }
}
</script>

<style scoped>
  .filter-menu{
    background-color: #FAFAFA;
  }

  .filter-menu-text{
    font-size: calc(10px + 0.2vw) !important;
  }

  button:hover{
    background-color: #1976d2 !important;
    color: white;
  }

  .v-menu__activator--active .room-filter{
    background-color: #1976d2 !important;
    color: white !important;
  }
</style>
