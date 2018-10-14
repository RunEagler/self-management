<template>
  <v-tooltip bottom>
    <v-btn slot="activator" icon @click.stop="dialog = true">
      <v-icon medium color="grey lighten-2">
        import_contacts
      </v-icon>
    </v-btn>
    <span>{{date}}</span>
    <v-dialog v-model="dialog" max-width="500px">
      <v-card>
        <v-card-title>
          Dialog
        </v-card-title>
        <v-card-text>
          <v-btn color="primary" dark @click.stop="dialog3 = !dialog3">Open Dialog 3</v-btn>
        </v-card-text>
        <v-card-actions>
          <v-btn color="primary" flat @click.stop="dialog2=false">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-tooltip>
</template>

<script>
export default {
  name: 'BookDate',
  data: () => {
    return {
      ['dialog' + this.date]: false
    }
  },
  props: {
    date: Number
  },
  computed: {
    getDialog: function () {
      return `dialog_${this.date}`
    }
  }

}
</script>

<style scoped>

</style>
