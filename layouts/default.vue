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
              <v-card-title class="text-h5 pt-8 pl-8">PROFILE</v-card-title>
              <div class="d-flex justify-center pt-6">
                <v-avatar size="100">
                  <img
                    alt="user"
                    src="~/assets/images/icon.jpg"
                  >
                </v-avatar>
              </div>
              <div class="text-center px-4 pt-4">
                <h3>Ryuki</h3>
                <div class="pt-4 px-10">
                  <p>
                    大阪在住 Webエンジニア.<br>
                    1996/11/26生まれ.<br>
                    日曜エンジニアが日々学んだことや詰まったことを備忘録として残していきます.<br>
                    今は主にNuxt.js,Laravelを勉強中.
                  </p>
                </div>
              </div>
              <!-- TODO: 記事ランキング機能の実装後具体的に着手していく -->
              <!-- <v-card-title class="text-h5 pt-16">TOP3 ARTICLE</v-card-title> -->
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
      menus: [
        {
          name: 'TOP',
          to: '/'
        },
        // {
        //   name: 'RANKING',
        //   to: '/'
        // },
        {
          name: 'CONTACT',
          to: '/contact'
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
