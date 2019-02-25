<template>
  <v-container>
    <v-layout row>
      <v-list-tile-sub-title class="card-title"> {{ headline }} </v-list-tile-sub-title>
    </v-layout>
    <v-layout row>
      <template grow v-if="isFlatRate">
        <span class="card-title price-avalibility-txt"> 
          ${{ room_prices[0] }} •  
        </span>
      </template>
      <template v-else>
        <span class="card-title price-avalibility-txt"> 
          ${{ room_prices[0] }}+ •
        </span>
      </template>
      <template v-if="isAvalibleToday">
        <span class="card-title pl-1 price-avalibility-txt"> avaliable today </span>
      </template>
      <template v-else-if="isAvalibleInFiveDays">
        <span class="card-title pl-1 price-avalibility-txt"> avaliable in 5 days </span>
      </template>
      <template v-else-if="isAvalibleInOneMonth">
        <span class="card-title pl-1 price-avalibility-txt"> avaliable in 1 month </span>
      </template>
    </v-layout>
    <v-layout row>
      <v-flex shrink pl-0 pb-0>
        <template v-for="room in occupiedRoom" xs1>
          <i class="material-icons room-icon orange--text text--darken-3">person</i>
        </template>
        <template v-for="room in available_room_count" xs1>
          <i class="material-icons room-icon orange--text text--darken-3 font-weight-medium">person_outline</i>
        </template>
      </v-flex>
      <v-flex grow pl-0 pb-0> 
        <v-list-tile-sub-title class='avaliable-room-txt'> 
          {{ available_room_count }} room avaliable
        </v-list-tile-sub-title>
      </v-flex>
    </v-layout>

  </v-container>
</template>

<script>
  import moment from 'moment'

  export default {
    name: "CardDescription",
    data() {
      return {
        occupiedRoom             : this.total_room_count - this.available_room_count,
        currentDate              : moment(),
        earliestAvailableDate    : moment(this.earliest_available_date),
        isFlatRate               : Math.max.apply(null,this. room_prices) == Math.min.apply(null,this.room_prices),
        isAvalibleToday          : moment(this.earliest_available_date).diff(this.currentDate,'days')   < 2,
        isAvalibleInFiveDays     : moment(this.earliest_available_date).diff(this.currentDate,'days')   < 5,
        isAvalibleInOneMonth     : moment(this.earliest_available_date).diff(this.currentDate,'months') < 2,
      }
    },
    props: {
      headline                : String,
      available_room_count    : Number,
      total_room_count        : Number,
      room_prices             : Array,
      earliest_available_date : String
    }
  }
</script>

<style scoped>
  .card-title {
    font-weight: 700;
  }

  .room-icon {
    font-size: 18px;
  }
  
  .price-avalibility-txt{
    font-weight: 400;
  }
  .avaliable-room-txt {
    color: #7e7e7e;
    font-weight: 500;
  }
</style>