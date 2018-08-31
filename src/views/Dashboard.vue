<template>
  <v-container fluid grid-list-lg>       
    <v-layout row wrap>
      <v-flex xs12 >
        <v-card >           
        <v-data-table
            :headers="headers"
            :items="employees"
            class="elevation-1"      
        >
            <template slot="headerCell" slot-scope="props">
            <v-tooltip bottom>
                <span slot="activator">
                {{ props.header.text }}
                </span>
                <span>
                {{ props.header.text }}
                </span>
            </v-tooltip>
            </template>
            <template slot="items" slot-scope="props">
            <td>{{ props.item.name }}</td>
            <td class="text-xs-right">{{ props.item.employee_id }}</td>
            <td class="text-xs-right">{{ props.item.dept }}</td>
            <td class="text-xs-right">{{ props.item.position }}</td> 

            <td class="justify-center layout px-0">
                    <v-tooltip bottom>
                        <v-icon
                            slot="activator"
                            small
                            class="mt-3 mr-2"
                            @click="editItem(props.item.employee_id)"             
                        >pageview
                        </v-icon>
                        <span>View Employee</span>
                    </v-tooltip>            
                </td>
            </template>
            
            <template slot="no-data">
                <v-alert :value="true" color="error" class="subheading" icon="warning">
                No data found in your databse 
                </v-alert>
            </template>     
        </v-data-table>          
          <v-card-text style="height: 100px; position: relative">
            <v-btn
              absolute
              dark
              fab
              top
              left
              color="orange darken-1"
              to="/new"
            >
              <v-icon>add</v-icon>
            </v-btn>
          </v-card-text>
        </v-card>
      </v-flex>      
    </v-layout>
  </v-container>
</template>

<script>
import db from "../components/firebaseInit";

export default {  
    name: 'dashboard',
    data () {
        return {
            employees: [],
            headers: [
                {
                    text: 'Employee Name',
                    align: 'center',
                    sortable: true,
                    value: 'name'
                },
                { text: 'Employee ID', value: 'employee_id' },            
                { text: 'Department', value: 'dept' },
                { text: 'Position', value: 'position' } ,
                { text: 'Actions', value: 'name', sortable: false }   
            ]
        }
    },
    created () {        
        db.settings({timestampsInSnapshots: true});
        db.collection("employees")
            .orderBy('dept')
            .get()
            .then(querySnapshot => {
                querySnapshot.forEach( doc => {                   
                    const data = {
                        'id' : doc.id,
                        'employee_id': doc.data().employee_id,
                        'name': doc.data().name,
                        'dept': doc.data().dept,
                        'position': doc.data().position
                    }
                    this.employees.push(data);
                });
            })
            .catch(function(error) {
                console.log("Error getting documents: ", error);
            });
    },
    methods: {
        editItem (id) {        
            this.$router.push('/view/' + id)
        }     
    }
}
</script>
