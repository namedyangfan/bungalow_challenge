<template>
  <v-flex sm12 md3 d-flex pt-1>
    <v-menu offset-y content-class="filter-menu" light z-index="1000"
      :close-on-content-click="false" max-width="300" nudge-bottom="10" max-height="150">
      <v-btn
        slot="activator"
        class="text-capitalize white room-filter"
      >
        <span text-capitalize>Avaliable Rooms</span>
      </v-btn>
      <v-flex pt-3 pl-4 pr-4>
        <v-range-slider
          v-model="avaliableRoomRange"
          :max="10"
          :min="1"
          always-dirty
          thumb-label="always"
          thumb-size="25"
        ></v-range-slider>
      </v-flex>
      <v-layout row>
        <v-flex grow/>
        <v-flex shrink>
          <v-btn flat medium 
            @click='filterAvaliableRooms(avaliableRoomRange)'>
            Apply
          </v-btn>
        </v-flex>
    </v-layout>
    </v-menu>
  </v-flex>
</template>

<script>
export default {
  name: 'RoomFilter',
  props: {
    selectedCity         : String,
    needClearFilter      : Boolean,
    isLoading            : Boolean,
    filterAvaliableRooms : Function,
    updateFilterStatus   : Function
  },

  data () {
    return {
      avaliableRoomRange  : [1,10],
    }
  },

  methods: {
  },

  watch: {
    needClearFilter: function(){
      this.avaliableRoomRange = [1,10];
    },

    isLoading: function(){
      this.filterAvaliableRooms(this.avaliableRoomRange)
    }
  }
}
</script>

<style scoped>
  .filter-menu{
    background-color: #FAFAFA;
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
