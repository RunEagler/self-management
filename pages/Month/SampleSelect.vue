<template>
  <v-combobox
    v-model="selectedItems"
    :items="icons"
    hide-selected
    label="Search for an option"
    multiple
  >
    <template
      slot="selection"
      slot-scope="{ item, parent}"
    >
      <v-chip
      >

          {{ item.txt }}
        <v-icon
          small
          @click="parent.selectItem(item)"
        >close</v-icon>
      </v-chip>
    </template>
    <template
      slot="item"
      slot-scope="{item }"
    >
        <v-chip>
          {{ item.txt }}
        </v-chip>
    </template>
  </v-combobox>
</template>

<script>
export default {
  name: 'select',
  data: () => ({
    icons: [
      { header: 'Select an option or create one' },
      {
        txt: 'Foo',
        color: 'blue'
      },
      {
        txt: 'Bar',
        color: 'red'
      }
    ],
    selectedItems: [
      {
        txt: 'Foo',
        color: 'blue'
      }
    ]
  })
}

</script>

<style scoped>

</style>
