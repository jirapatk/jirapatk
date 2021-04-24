<template>
  <v-card>
    <v-card-title>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      />
    </v-card-title>
    <v-data-table
      :headers="headers"
      :items="items"
      :search="search"
    />
  </v-card>
</template>

<script>
/* eslint-disable vue/require-prop-types */

export default {
  props: ['btnText', 'items', 'headers']
}
</script>
