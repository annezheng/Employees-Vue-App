<template>
 <v-container>
      <v-layout row class="mt-4" style="max-width: 700px; margin: auto;">
    <v-flex xs12>
  <v-card
    color="blue-grey darken-2"
    dark    
  >  
  <h3 class="subheading pt-2 ml-3">Edit Employee</h3>  
    <v-form 
        ref="form" 
        v-model="valid"
        @submit.prevent="updateEmployee">
      <v-container>
        <v-layout wrap>
          <v-flex xs12 md6>
            <v-text-field
              v-model="employee_id" 
              disabled                           
              box
              color="blue lighten-1"
              label="Employee ID"
              required
            ></v-text-field>
          </v-flex>
          <v-flex xs12 md6>
            <v-text-field
              v-model="name" 
              :rules="nameRules"             
              box
              color="blue lighten-1"
              label="Name"
              required
            ></v-text-field>
          </v-flex>

          <v-flex xs12 md6>
            <v-text-field
              v-model="dept" 
              :rules="nameRules"             
              box
              color="blue lighten-1"
              label="Department"
              required
            ></v-text-field>
          </v-flex>
          <v-flex xs12 md6>
            <v-text-field
              v-model="position" 
              :rules="nameRules"             
              box
              color="blue lighten-1"
              label="Position"
              required
            ></v-text-field>
          </v-flex>
        </v-layout>
      </v-container>
    
        <v-divider></v-divider>
        <v-card-actions>
            <v-btn        
            color="blue-grey darken-1"
            depressed
            :to="'/view/' + employee_id"        
            >
            <v-icon left>history</v-icon>
                Cancel
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn        
                color="blue-grey darken-1"     
                type="submit"
                :disabled="!valid"
            >
            <v-icon left>publish</v-icon>
                Update
            </v-btn>
        </v-card-actions>
    </v-form>
  </v-card>
  </v-flex>
  </v-layout>
  </v-container>
</template>

<script>
import db from "../components/firebaseInit";

export default {
    data () {   
        return {
            employee_id: null,        
            name: null,
            dept: null,
            position: null,
            nameRules: [
                v => !!v || 'This field is required'                
            ],
            valid: false
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
        updateEmployee () {
            this.dialog = false
            db.collection("employees")
            .where('employee_id', '==', this.$route.params.employee_id)
            .get()
            .then(querySnapshot => {
                querySnapshot.forEach( doc => {                    
                    doc.ref.update({                        
                        employee_id: this.employee_id,
                        name: this.name,
                        dept: this.dept,
                        position: this.position  

                    }) 
                    .then(() => {
                        this.$router.push({name: 'view-employee', params: {employee_id: this.employee_id}})  
                    })                                   
                })
            })                
        }
    }
    
}
</script>