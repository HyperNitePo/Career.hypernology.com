<template>
  <v-app class="grey lighten-3">
    <v-navigation-drawer v-model="nav" slide-x-transition fixed temporary class="hidden-md-and-up">
      <v-toolbar flat>
        <v-list>
          <v-list-tile>
            <v-list-tile-title class="title">
              導航
            </v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-toolbar>
      <v-divider></v-divider>
      <v-list dense>
        <template  v-for="(button,index) in buttons">
          <v-list-tile :key="index" :to="button.goto" @click.native="global.toTop">
            <v-list-tile-action>
              <v-icon>{{button.icon}}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title>{{button.name}}</v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </template>
      </v-list>
    </v-navigation-drawer>
      <v-toolbar dark app>
          <v-toolbar-side-icon  @click.stop="nav = !nav" class="hidden-md-and-up"><v-icon>menu</v-icon></v-toolbar-side-icon>
          <v-img src="/img/headlogo/HNlogo.png" alt="HyperNite" max-width="90px" max-height="40px"></v-img>
          <v-toolbar-title class="font-weight-light headline"></v-toolbar-title>
          <template v-if="$vuetify.breakpoint.mdAndUp">
              <template v-for="(button,index) in buttons">
                  <router-link :key="index" :to="button.goto"><v-btn flat >{{button.name}}</v-btn></router-link>
              </template>
              <v-spacer></v-spacer>
              <v-btn flat href="//www.hypernite.com">返回主頁</v-btn>
          </template>
      </v-toolbar>
      <v-content>
          <router-view></router-view>
      </v-content>
      <Footer></Footer>
  </v-app>
</template>
<script>
    import global from './global-func'
    import Footer from './components/Footer'
    export default {
        name: 'App',
        components: {
            Footer
        },
        data (){
            return {
                nav: false,
                global: global(),
                buttons: [
                    {
                        icon: 'home',
                        name: 'Home',
                        goto: '/'
                    },
                    {
                        icon: 'build',
                        name: 'button1',
                        goto: '/button1'
                    },
                    {
                        icon: 'games',
                        name: 'button2',
                        goto: '/about'
                    },
                ]
            }
        }
    }
</script>
