<template>
    <v-container fill-height>
      <v-layout row class="mt-4">
        <v-flex xs12 sm8 offset-sm2>        
          <v-list class="blue-grey lighten-1" dark>
          <v-subheader>Building Technologies </v-subheader>
          <v-list-tile>            
            <v-list-tile-content>
              <v-list-tile-title>VueJS</v-list-tile-title>              
            </v-list-tile-content>
            <v-list-tile-action>
              <v-btn icon ripple>
                <a href="https://vuejs.org/" target="_blank" style="text-decoration: none">
                <v-icon color="grey lighten-1">info</v-icon>
                </a>
              </v-btn>
              
            </v-list-tile-action>             
          </v-list-tile>
          <v-list-tile>
            <v-list-tile-content>
              <v-list-tile-title>Vuetify UI Framework</v-list-tile-title>  
            </v-list-tile-content> 
            <v-list-tile-action>
              <v-btn icon ripple>
                <a href="https://vuetifyjs.com/en/" target="_blank" style="text-decoration: none">
                <v-icon color="grey lighten-1">info</v-icon>
                </a>
              </v-btn>
            </v-list-tile-action>           
          </v-list-tile>
          <v-list-tile>
            <v-list-tile-content>
              <v-list-tile-title>Google Firestore</v-list-tile-title>  
            </v-list-tile-content>  
            <v-list-tile-action>
              <v-btn icon ripple>
                <a href="https://firebase.google.com/products/firestore/" target="_blank" style="text-decoration: none">
                <v-icon color="grey lighten-1">info</v-icon>
                </a>                
              </v-btn>
            </v-list-tile-action>          
          </v-list-tile>
        </v-list>          
        </v-flex>
      </v-layout>
    </v-container>
</template>