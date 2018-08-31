<template>
 <v-container>
      <v-layout row class="mt-4" style="max-width: 700px; margin: auto;">
    <v-flex xs12>
  <v-card
    color="blue-grey darken-1"
    dark
  > 
  <h3 class="subheading pt-2 ml-3">New Employee</h3>    
    <v-form 
        ref="form" 
        v-model="valid"
        @submit.prevent="saveEmployee">
      <v-container>
        <v-layout wrap>
          <v-flex xs12 md6>
            <v-text-field
              v-model="employee_id" 
              :rules="nameRules"                           
              box
              color="blue-grey lighten-2"
              label="Employee ID"
              required
            ></v-text-field>
          </v-flex>
          <v-flex xs12 md6>
            <v-text-field
              v-model="name" 
              :rules="nameRules"             
              box
              color="blue-grey lighten-2"
              label="Name"
              required
            ></v-text-field>
          </v-flex>

          <v-flex xs12 md6>
            <v-text-field
              v-model="dept" 
              :rules="nameRules"             
              box
              color="blue-grey lighten-2"
              label="Department"
              required
            ></v-text-field>
          </v-flex>
          <v-flex xs12 md6>
            <v-text-field
              v-model="position" 
              :rules="nameRules"             
              box
              color="blue-grey lighten-2"
              label="Position"
              required
            ></v-text-field>
          </v-flex>
        </v-layout>
      </v-container>
    
        <v-divider></v-divider>
        <v-card-actions>
            <v-btn        
            color="blue-grey darken-3"
            depressed
            to="/dashboard"        
            >
            <v-icon left>history</v-icon>
                Cancel
            </v-btn>
            <v-spacer></v-spacer>
            <v-btn        
                color="blue-grey darken-3"     
                type="submit"
                :disabled="!valid"
            >
            <v-icon left>add</v-icon>
                Add
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
    methods: {
        saveEmployee () {
            db.settings({timestampsInSnapshots: true});
            if (this.$refs.form.validate()) {
                db.collection('employees').add({
                    employee_id: this.employee_id,
                    name: this.name,
                    dept: this.dept,
                    position: this.position
                })
                .then(docRef => {
                    console.log(docRef);
                    this.$router.push('/dashboard');
                })
                .catch(error => console.log(error))
            }else {
                console.log('not validate')
            }            
        }
    }
}
</script>