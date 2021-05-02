<template>
  <v-container fluid>
    <h2>เพิ่มข้อมูลลูกค้า</h2>
    <BackButton />
    <v-card>
      <v-form @submit.prevent="createCustomer">
        <v-container>
          <v-row>
            <!-- ชื่อจริง -->
            <v-col
              cols="12"
              sm="6"
            >
              <v-text-field
                v-model="cus_firstname"
                required
                label="ชื่อจริง"
                prepend-icon="mdi-account"
              />
            </v-col>

            <!-- นามสกุล -->
            <v-col
              cols="12"
              sm="6"
            >
              <v-text-field
                v-model="cus_lastname"
                required
                label="นามสกุล"
                prepend-icon="mdi-account"
              />
            </v-col>

            <!-- เบอร์โทรศัพท์ -->
            <v-col
              cols="12"
              sm="6"
            >
              <v-text-field
                v-model="cus_phone"
                required
                label="เบอร์โทรศัพท์"
                prepend-icon="mdi-phone"
              />
            </v-col>
            <!-- สาขา -->
            <v-col
              cols="12"
              sm="6"
            >
              <v-text-field
                v-model="branch"
                :items="branch"
                label="สาขา"
                prepend-icon="mdi-map-marker"
              />
            </v-col>
          </v-row>
        </v-container>
        <v-btn class="primary ma-2" depressed type="submit">
          บันทึก
        </v-btn>
      </v-form>
    </v-card>
  </v-container>
</template>

<script>
export default {

  data () {
    return {
      cus_firstname: '',
      cus_lastname: '',
      cus_phone: '',
      branch: ''
    }
  },

  methods: {
    createCustomer () {
      this.$axios.post('customers', {
        cus_firstname: this.cus_firstname,
        cus_lastname: this.cus_lastname,
        cus_phone: this.cus_phone,
        branch: this.branch
      }).then((response) => {
        this.$router.push('./')
        this.$toast.show(response)
      }).catch((error) => {
        console.log(error)
      })
    }
  }
}
</script>
