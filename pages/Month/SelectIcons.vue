<template>
  <v-combobox
    v-model="selectIcons"
    :items="icons"
    @change="updateSelectedIcons"
    label="Select showing icons"
    multiple
    hide-selected
    clearable
    chips
  >
    <template slot="selection" slot-scope="{item,index,selected}">
      <v-chip close @input="remove(index)" >
        <v-icon>{{item.text}}</v-icon>
      </v-chip>
    </template>
    <template slot="item" slot-scope="{ index, item}">
      <v-chip color="indigo lighten-1" text-color="white">
        <v-avatar class="indigo darken-4">
          <v-icon>{{item.text}}</v-icon>
        </v-avatar>
        {{item.label}}
      </v-chip>
    </template>
  </v-combobox>
</template>

<script>
import {mapState, mapMutations, mapGetters} from 'vuex'

export default {
  name: 'SelectIcons',
  data: () => {
    return {
      icons: [
        {text: 'import_contacts', label: 'reading'},
        {text: 'work', label: 'work'},
        {text: 'directions_run', label: 'running'},
        {text: 'create', label: 'output'},
        {text: 'fitness_center', label: 'training'},
        {text: 'priority_high', label: 'idea'},
        {text: 'hearing', label: 'auditing'},
        {text: 'description', label: 'paper'},
        {text: 'music_note', label: 'music'}
      ],
      selectIcons: []
    }
  },
  mounted () {
    this.selectIcons = this.selectedIcons
  },
  computed: {
    ...mapState('date', ['selectedIcons']),
    ...mapMutations('date', ['setSelectedIcons']),
    ...mapGetters('date', ['getSelectedIcons'])
  },
  methods: {
    remove: function (iconIndex) {
      this.selectIcons.splice(iconIndex, 1)
    },
    updateSelectedIcons: function () {
      this.$store.commit('date/setSelectedIcons', this.selectIcons)
    }
  }
  /*
  watch: {
    selectIcons: function (newVal, oldVal) {
      // this.setSelectedIcons(newVal)
    }

  } */
}
</script>

<style scoped>

</style>
