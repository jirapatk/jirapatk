<template>
  <v-container fluid>
    <h2>เพิ่มสาขา</h2>
    <BackButton />
    <v-card>
      <v-form @submit.prevent="submit">
        <v-container>
          <v-row>
            <!-- ชื่อสาขา -->
            <v-col
              cols="12"
              sm="6"
            >
              <v-text-field
                v-model="name"
                required
                label="ชื่อเต็ม"
                prepend-icon="mdi-account"
              />
            </v-col>

            <!-- ชื่อย่อ -->
            <v-col
              cols="12"
              sm="6"
            >
              <v-text-field
                v-model="short_name"
                required
                label="ชื่อย่อ"
                prepend-icon="mdi-account"
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
      name: '',
      short_name: ''
    }
  },

  methods: {
    submit () {
      this.$axios.post('branches', {
        name: this.name,
        short_name: this.short_name
      }).then((response) => {
        this.$router.push('./')
        console.log(response)
        this.$toast.show(response)
      }).catch((error) => {
        console.log(error)
      })
    }
  }
}
</script>
