<template>
  <v-card v-bind:class="selectColor" text-darken-1>
    <v-card-title class="title" v-bind:class="{saturday : dateState.isSaturday,sunday : dateState.isSunday}">
      {{dateState.date}}
    </v-card-title>
    <v-card-text>
      <v-layout row wrap>
        <v-flex  md3 sm4 xs6 v-for="(icon,i) in this.selectedIcons" :key="i">
          <v-icon medium color="grey lighten-2" v-bind:class="{invisible :dateState.dateType == 'exclude_date'}">
            {{icon.text}}
          </v-icon>
        </v-flex>
      </v-layout>
    </v-card-text>
    <v-card-actions>
      <v-icon v-bind:class="{invisible :dateState.dateType != 'past_date'}">check</v-icon>
      <v-btn
        color="red lighten-2"
        icon
      >
        <v-icon>view_comfy</v-icon>
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>

// import BookDate from './BookDate'
// import {mapMutations, mapGetters} from 'vuex'

export default {
  name: 'Date',
  data: () => {
    return {
      icons: ['import_contacts', 'work', 'directions_run', 'create', 'fitness_center', 'priority_high', 'hearing', 'description', 'music_note'],
      selectedIcons: [
        {text: 'import_contacts', label: 'reading'},
        {text: 'work', label: 'work'},
        {text: 'directions_run', label: 'running'},
        {text: 'create', label: 'output'},
        {text: 'fitness_center', label: 'training'},
        {text: 'priority_high', label: 'idea'},
        {text: 'hearing', label: 'auditing'},
        {text: 'description', label: 'paper'},
        {text: 'music_note', label: 'music'}
      ]
    }
  },
  props: {
    dateState: Object
  },
  // components: {
  //   BookDate
  // },
  computed: {
    // ...mapGetters('date', ['getSelectedIcons']),

    selectColor: function () {
      let colorObj
      switch (this.dateState.dateType) {
        case 'current_date':
          colorObj = {
            'current-date': true
          }
          break
        case 'future_date':
          colorObj = {
            'future-date': true
          }
          break
        case 'past_date':
          colorObj = {
            'past-date': true
          }
          break
        case 'exclude_date':
          colorObj = {
            'exclude-date': true
          }
          break
      }
      return colorObj
    }
  },
  methods: {
    // ...mapMutations('date', ['setDetailDialog'])

  }
}
</script>

<style scoped>
  .invisible {
    visibility: hidden;
  }

  .saturday {
    color: #009dec;
  }

  .sunday {
    color: #ff0000;
  }

  .current-date {
    background-color: #FFF9C4;
  }

  .future-date {
    background-color: #F5F5F5;
  }

  .past-date {
    background-color: #BDBDBD;
  }

  .exclude-date {
    background-color: #424242
  }
</style>
