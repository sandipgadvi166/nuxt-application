<template>
  <v-app>
    <v-app-bar app fixed flat dark scroll-target="#scrolling-techniques-6">
      <v-app-bar-nav-icon @click="drawer = true"> </v-app-bar-nav-icon>

      <v-title class="text-center pl-4">
        <h1 class="font-weight-bold">Account Book</h1>
      </v-title>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" absolute temporary>
      <v-list nav dense>
        <v-list-item-group v-model="group">
          <v-list-item to="/">
            <v-list-item-icon>
              <v-icon>mdi-home</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Home</v-list-item-title>
          </v-list-item>

          <v-list-item to="/account">
            <v-list-item-icon>
              <v-icon>mdi-account</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Account Book</v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
    <nuxt />
  </v-app>
</template>

<script>
export default {
  head: {
    title: 'Billing For Pet Hospital',
    meta: [
      {
        charset: 'uft-8',
      },
      {
        name: 'description',
        content: 'Pet Hospital application to manag your billing account',
      },
      {
        hid: 'keyword',
        name: 'keyword',
        content:
          'billing pet care animal doctor, dog and cat treatment, dog rabise dose, cat teatment, cow and bull treatment, vaccination',
      },
    ],
  },
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/',
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire',
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js',
    }
  },
}
</script>
