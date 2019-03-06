<template>
    <v-card flat tile height="100%" class="pa-0" >
      <v-layout column fill-height>
        <v-container fluid fill-height grey lighten-5>
          <v-layout>
            <v-flex d-flex justify-center align-center class="text-xs-center">
              <v-progress-circular :size="100" color="primary" indeterminate></v-progress-circular>
            </v-flex>
          </v-layout>
        </v-container>
      </v-layout>
    </v-card>
</template>

<script>
export default {
  name: 'LoadingState'
}
</script>

<style>

</style>
