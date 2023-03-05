<template>
    <v-app>
        <v-app-bar
          app
        >
            <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
            <v-toolbar-title>{{ title }}</v-toolbar-title>
            <v-spacer />
            <v-spacer />
            <!-- <div style="margin-top:300px !important" v-if="$auth.loggedIn">
                {{ $auth.user }}
                <v-btn text>Logout</v-btn>
            </div> -->
            <div>
                <v-btn class="mr-5" text to="/login">Login</v-btn>
                <v-btn class="mr-5" text to="/signup">Register</v-btn>
            </div>
        </v-app-bar>
        <v-toolbar />
        <main>
          <slot />
        </main>
    </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
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
      title: 'MOTOTRAK',
    }
  },
}
</script>

<style lang="sass">
</style>