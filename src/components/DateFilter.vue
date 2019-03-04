<template>
  <v-menu ref="menu" offset-y content-class="filter-menu" light 
    :close-on-content-click="false" max-width="400" nudge-bottom="10">
    <v-btn
      slot="activator"
      class="text-capitalize white room-filter"
    >
      <span text-capitalize class="filter-menu-text">Move-in Date</span>
    </v-btn>
    <v-flex>
      <v-date-picker
        ref          = "picker"
        no-title
        v-model      = "moveInDate"
        show-current = "2019-03-13"
        v-on:change  = "updateMoveInDate"
        :min         = "currentDate"
      >
      </v-date-picker>
    </v-flex>
  </v-menu>
</template>

<script>
import _      from 'lodash'
import moment from 'moment'

export default {
  name: 'DateFilter',
  props: {
    needClearFilter      : Boolean,
    isLoading            : Boolean,
    filterMoveInDate     : Function
  },

  data () {
    return {
      moveInDate  : null,
      currentDate : moment().format("YYYY-MM-DD"),
      filterMin   : this.$route.query.availableRoomsMin || 1,
      filterMax   : this.$route.query.availableRoomsMax || 10
    }
  },

  methods: {
    getMoveInDate: function(){
      this.$route.query.moveInDate?(
        this.moveInDate = moment(this.$route.query.moveInDate).format("YYYY-MM-DD")
        ):(
        this.moveInDate = moment().format("YYYY-MM-DD")
      )
    },

    updateRouterParams: function(){
      this.$router.replace({ 
        query: {...this.$route.query, moveInDate: this.moveInDate}
      })
    },

    debounceFilterMoveInDate:_.debounce(function() {
      this.filterMoveInDate(this.moveInDate)
    }, 500),

    updateMoveInDate: function(){
      this.updateRouterParams()
      this.debounceFilterMoveInDate()
    },
  },

  created() {
    this.getMoveInDate()
  },
  watch: {
    needClearFilter: function(){
      this.moveInDate = this.currentDate
      this.updateRouterParams();
    },

    isLoading: function(){
      this.isLoading?(
        null
      ):(
        this.filterMoveInDate(this.moveInDate)
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
