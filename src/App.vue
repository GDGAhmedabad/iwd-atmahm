<template>
  <v-app class="white">
    <v-navigation-drawer
      v-model="drawer"
      :clipped="$vuetify.breakpoint.lgAndUp"
      fixed
      app
      disable-resize-watcher
      disable-route-watcher
      class="hidden-md-and-up"
    >
      <v-flex xs12 class="pl-3 pt-5">
        <v-img
              :src="data.eventLogo"
              :lazy-src="data.eventLogo"
              width="5vh">
              <v-layout
                  slot="placeholder"
                  fill-height
                  align-center
                  justify-center
                  ma-0
              >
                  <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
              </v-layout>
        </v-img>
        <p class="google-font mt-2">{{ data.navTitle }}</p>
        
      </v-flex>


      <v-list class="pt-0" dense>
        <v-divider></v-divider>
        <v-list-tile
            v-for="item in items"
            :key="item.title"
            router :to="item.route"
        >   
            <v-list-tile-action>
                <v-icon>{{ item.icon }}</v-icon>
            </v-list-tile-action>

            <v-list-tile-content>
                <v-list-tile-title>{{ item.title }}</v-list-tile-title>
            </v-list-tile-content>
        </v-list-tile>
      </v-list>  
    </v-navigation-drawer>

    <v-toolbar
      :clipped-left="$vuetify.breakpoint.lgAndUp"
      color="white"
      app
      scroll-off-screen
      fixed
    >
      <v-toolbar-side-icon class="hidden-md-and-up" @click.stop="drawer =!drawer"></v-toolbar-side-icon>
      <v-toolbar-title class="ml-0 pl-1 mr-1">   
        <span class="google-font">{{data.navTitle}}</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn class="mx-1 hidden-sm-and-down google-font" 
        flat v-for="(item, i) in items" 
        :key="i" 
        router  
        style="text-transform: capitalize;"    
        :to="item.route">
        {{item.title}}
      </v-btn>

    </v-toolbar>

    <v-content class="mt-0 mb-0 pa-0">
      <router-view></router-view>
    </v-content>

    <bottomNavbar/>
    <cofooter/>
  </v-app>
</template>

<script>

import bottomNavbar from './components/bottom-footer'
import cofooter from './components/footer'
import homeData from '@/assets/data/home.json'

export default {
  name: 'App',
  components: {
    bottomNavbar,
    cofooter,
  },
  data: () => ({
      drawer: false,
      data:homeData,
      items: [
            { title: 'Home', icon: 'dashboard', route:"/home" },
            { title: 'Attending', icon: 'rounded_corner', route:"/attending" },
            { title: 'Agenda', icon: 'toc', route:"/agenda" },
            { title: 'Speakers', icon: 'group', route:"/speakers" },
            { title: 'Teams', icon: 'person', route:"/team" }
        ],
    }),
    methods:{
    }
}
</script>
