<template> 
  <v-app> 
    <Navbar/>
    <v-content>
      <router-view />
    </v-content>    
    <v-footer
    dark
    height="auto">
    <v-card
      class="flex"
      flat
      tile>      
      <v-card-actions class="grey darken-3 justify-center">
        &copy;2018 — <strong>Vuetify</strong>
      </v-card-actions>
    </v-card>
  </v-footer>
  </v-app>
</template>

<script>
import Navbar from './views/Navbar'

export default {
  components: {
    Navbar
  } 
}
</script>
