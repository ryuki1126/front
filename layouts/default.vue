<template>
  <v-app :dark="setTheme">
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
      color="main"
    >
      <v-toolbar-title v-text="title" class="pr-10" />
      <div class="flex justify-center">
        <v-btn 
          v-for="(menu, i) in menus"
          :key="i" 
          text
          x-large
          
        >
          <nuxt-link class="pointer" tag="div" :to="`${menu.to}`">
            {{ menu.name }}
          </nuxt-link>
        </v-btn>
      </div>
      <div class="px-4 pt-6">
      <v-spacer />
      <v-switch
        v-model="goDark"
        color="warning"
        :prepend-icon="themeIcon"
      >
      </v-switch>
      </div>
    </v-app-bar>
    <v-main>
      <div class="px-10 background">
        <v-row class="pt-5">
          <v-col cols="9" class="px-5">
            <Nuxt />
          </v-col>
          <v-col cols="3">
            <v-card
              height=100%
              elevation="2"
              class="my-3"
            >
              <v-card-title class="text-h5">PROFILE</v-card-title>
              <div class="d-flex justify-center pt-6">
                <v-avatar size="100">
                  <img
                    alt="user"
                    src="https://cdn.pixabay.com/photo/2020/06/24/19/12/cabbage-5337431_1280.jpg"
                  >
                </v-avatar>
              </div>
              <div class="text-center px-4 pt-4">
                <h3>Ryuki</h3>
                <div class="pt-4">
                  <p>
                    大阪在住 Webエンジニア<br>
                    1996/11/26生まれ<br>
                    Vue.js,Nuxt.js,Laravel等モダンな技術を学んで得た知識をアウトプットしていきます
                  </p>
                </div>
              </div>
              <v-card-title class="text-h5 pt-16">TOP3 ARTICLE</v-card-title>
            </v-card>
          </v-col>
        </v-row>  
      </div>
    </v-main>
    <v-footer
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      goDark: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      menus: [
        {
          name: 'TOP',
          to: '/'
        },
        {
          name: 'RANKING',
          to: '/'
        },
        {
          name: 'CONTACT',
          to: '/'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Webエンジニアの備忘録'
    }
  },
  computed: {
    themeIcon() {
      return this.goDark ? 'mdi-weather-night' : 'mdi-weather-sunny'
    },
    setTheme() {
      if (this.goDark == true) {
        return (this.$vuetify.theme.dark = true);
      } else {
        return (this.$vuetify.theme.dark = false);
      }
    }
  }
}
</script>
