<template>
  <v-toolbar app scroll-toolbar-off-screen scroll-off-screen clipped-left>
    <v-toolbar-side-icon>
      <v-tooltip bottom>
        <v-icon
          slot="activator"
        >settings
        </v-icon>
        <span>preference</span>
      </v-tooltip>
    </v-toolbar-side-icon>
    <v-toolbar-title>
      SELF-MANAGEMENT
    </v-toolbar-title>
    <v-spacer></v-spacer>
    <v-toolbar-items class="hidden-sm-and-down">
      <v-btn flat :to="{name: 'Career'}">Month</v-btn>
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>
export default {
  name: 'custom-toolbar'
}
</script>
