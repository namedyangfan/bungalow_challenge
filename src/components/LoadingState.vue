<template>
  <v-container fill-height>
    <div class="text-xs-center center-loading">
      <v-progress-circular :size="100" color="primary" indeterminate>
      </v-progress-circular>
    </div>
  </v-container>
</template>

<script>
export default {
  name: 'LoadingState'
}
</script>

<style>
  .center-loading{
    padding-left: 45%;
  }
</style>
