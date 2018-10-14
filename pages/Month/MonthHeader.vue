<template>
    <v-layout row text-xs-center>
      <v-flex xs1 row v-for="j in 12" :key="j">
        <v-card color="yellow lighten-4" class="title" v-if="j == current_month">
         <v-card-text class="px-0">
           <v-btn flat>{{month[j-1]}}</v-btn>
         </v-card-text>
        </v-card>
        <v-card color="blue lighten-5" class="title" v-else>
          <!--
          <v-badge left>
            <span slot="badge">4.5</span>
            <v-icon large color="grey lighten-1">create</v-icon>
          </v-badge>
          -->
          <v-card-text class="px-0">
            <v-btn flat>
              {{month[j-1]}}
            </v-btn>
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
</template>

<script>
export default {
  name: 'MonthHeader',
  data: () => {
    return {
      month: ['January', 'Feburary', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
    }
  },
  props: {
    current_month: Number
  }
}
</script>

<style scoped>

</style>
