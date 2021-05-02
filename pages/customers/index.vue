<template>
  <v-container>
    <h2>ข้อมูลลูกค้า</h2>
    <v-col class="text-right">
      <v-btn class="primary ma-2 justify-right" to="/customer/create" depressed nuxt>
        เพิ่ม
        <v-icon
          right
          dark
        >
          mdi-plus
        </v-icon>
      </v-btn>
      <v-btn class="primary ma-2 justify-right" to="/customer/create" depressed nuxt>
        พิมพ์
        <v-icon
          right
          dark
        >
          mdi-printer
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
        :sort-desc.sync="sortDesc"
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
    const customers = await $axios.$get('customers')
    return {
      sortBy: 'id',
      sortDesc: true,
      search: '',
      headers: [
        {
          text: 'รหัสลูกค้า',
          align: 'start',
          sortable: true,
          filterable: true,
          value: 'id'
        },
        { text: 'ชื่อ', value: 'cus_firstname' },
        { text: 'นามสกุล', value: 'cus_lastname' },
        { text: 'เบอร์โทรศัพท์', value: 'cus_phone' },
        { text: 'สาขา', value: 'branch.name' },
        { text: 'สร้างเมื่อ', value: 'created_at' },
        { text: 'Actions', value: 'actions', sortable: false }
      ],
      customer: customers
    }
  }
}
</script>
