<template>
  <v-container>
    <h2>สาขา</h2>
    <v-col class="text-right">
      <v-btn class="primary ma-2 justify-right" to="/branches/create" depressed nuxt>
        เพิ่ม
        <v-icon
          right
          dark
        >
          mdi-plus
        </v-icon>
      </v-btn>
    </v-col>
    <v-card>
      <v-card-title>
        ค้นหา
        <v-spacer />
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Search"
          single-line
        />
      </v-card-title>
      <v-data-table
        :sort-by.sync="sortBy"
        :headers="headers"
        :items="customer"
        :search="search"
      >
        <template #[`item.actions`]="{ item }">
          <v-icon
            small
            class="mr-2"
            @click="editItem(item)"
          >
            mdi-pencil
          </v-icon>
          <v-icon
            small
            @click="deleteItem(item)"
          >
            mdi-delete
          </v-icon>
        </template>
      </v-data-table>
    </v-card>
  </v-container>
</template>

<script>
export default {
  async asyncData ({ $axios }) {
    const customers = await $axios.$get('branches')
    return {
      sortBy: 'id',
      search: '',
      headers: [
        {
          text: 'เลขที่',
          align: 'start',
          sortable: true,
          filterable: true,
          value: 'id'
        },
        { text: 'สาขา', value: 'name' },
        { text: 'ชื่อย่อ', value: 'short_name' }
      ],
      customer: customers
    }
  }
}
</script>
