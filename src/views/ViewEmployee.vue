<template>
<v-container>
  <v-layout row class="mt-4" style="max-width: 700px; margin: auto;">
    <v-flex xs12>
        <v-card color="blue-grey darken-1" class="white--text elevation-20">
            <v-layout>
            <v-flex xs5>
                <v-card-media                
                :src="`https://unsplash.it/150/300?image=${Math.floor(Math.random() * 100) + 1}`"
                height="150px"                                 
                ></v-card-media>
            </v-flex>
            <v-flex xs7>
                <v-card-title primary-title>
                <div>
                    <div class="headline">{{name}}</div>
                    <div>{{position}}</div>
                    <div>{{dept}}</div>                    
                </div>                
                </v-card-title>
            </v-flex>
            </v-layout>
            <v-divider light></v-divider>
                <v-card-actions class="pa-3">      
                <v-btn flat color="indigo lighten-4" to="/dashboard">Go Back</v-btn>
                <v-dialog v-model="dialog" persistent max-width="290">
                    <v-btn slot="activator" flat color="orange">Delete</v-btn>
                    <v-card>
                        <v-card-title class="headline">Are you sure you want to delete?</v-card-title>
                        <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn color="green darken-1" flat @click.native="dialog = false">No</v-btn>
                        <v-btn color="green darken-1" flat @click.native="deleteEmployee">Yes</v-btn>
                        </v-card-actions>
                    </v-card>
                </v-dialog>   
            </v-card-actions>
            <v-card-text style="height: 50px; position: relative">
            <v-btn
              absolute
              dark
              fab
              top
              right
              color="orange darken-1"
              :to="'/edit/'+ employee_id"
            >
              <v-icon>edit</v-icon>
            </v-btn>            
          </v-card-text>     
        </v-card>
    </v-flex>
  </v-layout>
  </v-container>
</template>

<script>
import db from "../components/firebaseInit"

export default {
    data () {
        return {
            employee_id: null,
            name: null,
            dept: null,
            position: null,
            dialog: false
        }
    },
    beforeRouteEnter (to, from, next) {
        db.settings({timestampsInSnapshots: true});
        db.collection("employees")
            .where('employee_id', '==', to.params.employee_id)
            .get()
            .then(querySnapshot => {
                querySnapshot.forEach( doc => {                    
                    next(vm => {
                        vm.employee_id = doc.data().employee_id;
                        vm.name = doc.data().name;
                        vm.dept = doc.data().dept;
                        vm.position = doc.data().position;
                    })                    
                })
            })            
    },
    watch: {
        '$route': 'fetchData'
    },
    methods: {
        fetchData () {
            db.collection("employees")
            .where('employee_id', '==', this.$route.params.employee_id)
            .get()
            .then(querySnapshot => {
                querySnapshot.forEach( doc => {                    
                    this.id = doc.id,
                    this.employee_id = doc.data().employee_id,
                    this.name = doc.data().name,
                    this.dept = doc.data().dept,
                    this.position = doc.data().position                    
                })
            })            
        },
        deleteEmployee () {
            this.dialog = false
            db.collection("employees")
            .where('employee_id', '==', this.$route.params.employee_id)
            .get()
            .then(querySnapshot => {
                querySnapshot.forEach( doc => {                    
                    doc.ref.delete()  
                    this.$router.push('/dashboard')                
                })
            })                
        }
    }
}
</script>
