<template>
  <v-container fill-height>
    <v-layout row wrap align-center class="center-loading">
      <v-progress-circular :size="100" color="primary" indeterminate>
      </v-progress-circular>
    </v-layout >
  </v-container>
</template>

<script>
export default {
  name: 'LoadingState'
}
</script>

<style>

</style>
