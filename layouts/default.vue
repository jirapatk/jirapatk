<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      fixed
      app
    >
      <v-list>
        <v-list-item class="px-2">
          <div class="my-6 mx-2">
            <h1>Nuxt</h1>
          </div>
        </v-list-item>

        <v-list-item link>
          <v-list-item-content>
            <v-list-item-title class="title">
              {{ user.Name }}
            </v-list-item-title>
            <v-list-item-subtitle>{{ user.email }}</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>
      </v-list>
      <v-divider />

      <v-list
        nav
        dense
      >
        <v-list>
          <v-list-item
            v-for="(item, i) in items"
            :key="i"
            :to="item.to"
            router
            exact
            color="primary"
          >
            <v-list-item-action>
              <v-icon>{{ item.icon }}</v-icon>
            </v-list-item-action>
            <v-list-item-content>
              <v-list-item-title v-text="item.title" />
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-list>

      <template #append>
        <div class="pa-2">
          <v-list-item block color="primary" @click="logout">
            Logout
          </v-list-item>
        </div>
      </template>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
      dark
      color="primary"
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title v-text="title" />
      <v-spacer />
    </v-app-bar>
    <v-main>
      <!-- <v-container class="mx-6"> -->
      <v-container class="my-6">
        <nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
/* eslint-disable vue/require-prop-types */

export default {
  middleware: 'auth',
  data () {
    return {
      user: this.$auth.user,
      clipped: false,
      drawer: false,
      fixed: true,
      items: [
        {
          icon: 'mdi-apps',
          title: 'หน้าหลัก',
          to: '/'
        },
        {
          icon: 'mdi-account-check',
          title: 'ลูกค้า',
          to: '/customers'
        },
        {
          icon: 'mdi-account-settings-outline',
          title: 'ผู้ใช้งานระบบ',
          to: '/users'
        },
        {
          icon: 'mdi-file-document',
          title: 'ใบเสนอราคา',
          to: '/quotations'
        },
        {
          icon: 'mdi-marker-check',
          title: 'สาขา',
          to: '/branches'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Suriya Group'
    }
  },
  methods: {
    async logout () {
      await this.$auth.logout()
      this.$router.push('/login')
    }
  }
}
</script>

<style>

  html
#app {
  font-family: 'FC Iconic', sans-serif;
}
</style>
