<template>
  <v-app id="inspire">
    <v-main>
      <v-container fluid fill-height>
        <v-layout align-center justify-center max-height>
          <v-flex xs12 sm8 md4>
            <v-card class="elevation-12" @keyup.enter="login">
              <v-toolbar dark color="primary">
                <v-toolbar-title>
                  เข้าสู่ระบบ
                </v-toolbar-title>
                <v-spacer />
              </v-toolbar>
              <v-card-text>
                <v-form>
                  <v-text-field
                    v-model="email"
                    prepend-icon="mdi-account"
                    name="username"
                    label="Username"
                    type="text"
                  />
                  <v-text-field
                    id="password"
                    v-model="password"
                    prepend-icon="mdi-key"
                    name="password"
                    label="Password"
                    type="password"
                  />
                </v-form>
              </v-card-text>

              <v-card-actions>
                <v-spacer />
                <v-btn color="primary" @click="login">
                  Login
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
/* eslint-disable no-console */
import Swal from 'sweetalert2/dist/sweetalert2.js'

export default {
  layout: 'auth',
  data () {
    return {
      email: '',
      password: ''
    }
  },
  methods: {
    async login (e) {
      e.preventDefault()
      const payload = {
        identifier: this.email,
        password: this.password
      }
      try {
        await this.$auth.loginWith('local', {
          data: payload
        })
        this.$auth.setUser('user.data')
        this.$router.push('/')
        console.log()
      } catch (e) {
        this.$router.push('/login')
        console.log(e)
        Swal.fire({
          title: 'ไม่สามารถเข้าสู่ระบบ!',
          text: 'Username หรือ Password ไม่ถูกต้อง',
          type: 'error'
        })
      }
    }
  }
}
</script>
