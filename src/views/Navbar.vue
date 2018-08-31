<template>
    <div>
        <v-toolbar color='secondary' dark>
            <v-toolbar-side-icon 
                @click.stop="drawer = !drawer"
                class="hidden-sm-and-up">
            </v-toolbar-side-icon>
            <v-toolbar-title>
                <router-link to="/" tag="span" style="cursor: pointer">Employee Manager</router-link>
            </v-toolbar-title>
            <v-spacer></v-spacer>
            <v-toolbar-items class="hidden-xs-only">
            <v-btn flat to="/dashboard">Dashboard</v-btn> 
            <v-btn flat to="/new">New Employee</v-btn> 
            <v-btn flat to="/about">About</v-btn>            
            </v-toolbar-items>
        </v-toolbar>
        <v-navigation-drawer
            v-model="drawer"
            absolute
            temporary
            class="hidden-sm-and-up">
            <v-list class="pa-1">
                <v-list-tile avatar to='/'>
                <v-list-tile-avatar>
                    <img src="https://cdn.pixabay.com/photo/2016/10/28/11/57/tic-tac-toe-1777859_1280.jpg">
                </v-list-tile-avatar>
                <v-list-tile-content>
                    <v-list-tile-title>Employee Manager</v-list-tile-title>
                </v-list-tile-content>
                </v-list-tile>
            </v-list>
            <v-list class="pt-0" dense>      
                <v-divider /> 
                <v-list-tile to='/dashboard'>
                <v-list-tile-action>
                    <v-icon>dashboard</v-icon>
                </v-list-tile-action>
                <v-list-tile-content>
                    <v-list-tile-title>Dashboard</v-list-tile-title>
                </v-list-tile-content> 
                </v-list-tile>              
                <v-list-tile to='/new'>
                <v-list-tile-action>
                    <v-icon>add_circle</v-icon>
                </v-list-tile-action>
                <v-list-tile-content>
                    <v-list-tile-title>New Employee</v-list-tile-title>
                </v-list-tile-content>
                </v-list-tile>
                <v-list-tile to='/about'>
                <v-list-tile-action>
                    <v-icon>question_answer</v-icon>
                </v-list-tile-action>
                <v-list-tile-content>
                    <v-list-tile-title>About</v-list-tile-title>
                </v-list-tile-content>
                </v-list-tile>
            </v-list>
        </v-navigation-drawer>
    </div>
</template>

<script>
  export default {
    data () {
      return {
        drawer: null,
        items: [
          { title: 'Home', icon: 'dashboard' },
          { title: 'About', icon: 'question_answer' }
        ]
      }
    }
  }
</script>

    