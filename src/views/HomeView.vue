<template>
<div class="pink lighten-5">
   <v-card-actions>
<h1 style="color:blue"><i>welcome {{data}}</i></h1> 
  <v-spacer></v-spacer>
<v-btn color="primary" v-on:click="logout()">LOGOUT</v-btn>
</v-card-actions>
<form>
<h1>CAR FORM</h1>
<br>
<label><b>CAR NAME </b></label>
      <v-row>
        <v-col
          cols="6"
          sm="3"
        >
        <v-text-field
        v-model="car_name"
         :rules="rules.req"
        outlined
      ></v-text-field>
        </v-col>
       </v-row>
        <v-row>
          <v-col
          cols="6"
          sm="3"
        >
        <label><b>COLOUR </b></label>
          <v-text-field
            v-model="colour"
             outlined
            :rules="rules.req"
          ></v-text-field>
        </v-col>
      </v-row>

         <v-row>
          <v-col
          cols="6"
          sm="3"
        >
        <label><b>PRICE </b></label>
          <v-text-field
            v-model="price"
             v-on:keypress="NumbersOnly"
             outlined
          ></v-text-field>
        </v-col>
      </v-row>

         <v-row>
          <v-col
          cols="6"
          sm="3"
        >
        <label><b>YEAR </b></label>
          <v-text-field
               v-model="year"
               v-on:keypress="NumbersOnly"
               outlined
          ></v-text-field>
        </v-col>
      </v-row>

  <v-btn v-if="!isEdit" depressed color ="primary" v-on:click="onsubmit()">SUBMIT</v-btn>
     <v-btn v-else depressed color ="primary" v-on:click=" updateDataInForm()">UPDATE</v-btn>
</form>

<h1><center>CAR TABLE</center></h1>
    <v-simple-table dark>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            CARNAME
          </th>
          <th class="text-left">
            COLOUR
          </th>
           <th class="text-left">
           ID
          </th>
            <th class="text-left">
            PRICE
          </th>
          <th class="text-left">
           YEAR
          </th>
            <th class="text-left">
           UPDATE ACTION
          </th>
          <th class="text-left">
           DELETE ACTION
          </th>
       </tr>
      </thead>
       <tbody>
     <tr v-for="(item,index) in list" v-bind:key="item.id">
      <td>{{ item.car_name }}</td>
       <td>{{ item.colour }}</td>
        <td>{{ item.id }}</td>
           <td>{{ item.price }}</td>
          <td>{{ item.year }}</td>
        <td> <v-btn depressed color ="teal" @click="updateData(index)">UPDATE
            </v-btn></td>
           <td><v-btn depressed color ="error" v-on:click="deleteData(item.id)">DELETE</v-btn></td>
          
       </tr>
         </tbody>
    </template>
  </v-simple-table>
  <hello-world />
  </div>
</template>

<script>
  import HelloWorld from '../components/HelloWorld'
  import Vue from 'vue'
  import axios from 'axios'
  import VueAxios from 'vue-axios'
  Vue.use(VueAxios,axios)
  export default {

 data(){
      return {
      data:'',
       rules: {
          req: [val => (val || '').length > 0 || 'Mandatory Field', val => (!val) || /^[a-zA-Z\s]*$/.test(val) || 'Please type only alphabets'],
      },
        car_name:'',
        colour:'',
        price:'',
        year:'',
        list:[],
        rowindex:0,
        isEdit: false,
      }
      

 },
 methods: {
   NumbersOnly: (event) => {
      let keyCode = event.keyCode;
      if (keyCode < 48 || keyCode > 57) {
        event.preventDefault();
      }
    },
getData(){
  this.data = localStorage.getItem('loggedin')
  this.data = JSON.parse(this.data)
  console.log(this.data)
this.axios.get('http://127.0.0.1:3333/cars')
       .then((res) => {
        this.list=res.data
        console.log(this.list);
       })
       
     },
     onsubmit(){

        this.axios.post('http://127.0.0.1:3333/cars', {
          car_name: this.car_name,
          colour: this.colour,
          price: this.price,
          year: this.year,
        })
        .then((response) => {
          const data = response.data;
          this.list.push(data);
          this.car_name = "";
          this.colour = "";
          this.price= "";
          this.year="";
        });
     },

  updateData(id){

  this.isEdit = true;
  this.car_name= this.list[id].car_name;
  this.colour=this.list[id].colour;
  this.price=this.list[id].price;
  this.year=this.list[id].year;
  
  this.rowindex=id;
  },

  updateDataInForm()
  {
      this.axios.patch('http://127.0.0.1:3333/cars',{
        
        id: this.list[this.rowindex].id,
        car_name:this.car_name,
        colour:this.colour,
        price:this.price,
        year:this.year
        })
      this.list[this.rowindex].car_name=this.car_name;
      this.list[this.rowindex].colour = this.colour;
      this.list[this.rowindex].price = this.price;
      this.list[this.rowindex].year = this.year;

      this.isEdit=false;
  },

 deleteData(id){
 this.axios.delete('http://127.0.0.1:3333/cars/'+id)
      .then(()=>{
         this.getData();
      })
    },
    logout(){
      alert('logged out')
      this.$router.push('/')
    },
  },

   mounted(){
      this.getData(); 
    },

  
    name: 'HomeView',

    components: {
      HelloWorld,
    },
  }
</script>
