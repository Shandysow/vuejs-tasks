<template>
<div class="pink lighten-5">
<form>
<h1><center>FORM REGISTRATION</center></h1>
<br>
      <v-row>
        <v-col
          cols="12"
          sm="6"
        >
            <v-text-field
        v-model="name"
        :rules="rules.req"
        label="NAME"
        filled
        required
      ></v-text-field>
        </v-col>
        
          <v-col
          cols="12"
          sm="6"
        >
          <v-text-field
            v-model="email"
             label="E-MAIL ID"
            :rules="[rules.required, rules.email]"
             filled
          ></v-text-field>
        </v-col>
      </v-row>

 <label><b><i>PASSWORD-LENGTH</i></b></label>
       <v-row>
       <v-col
          cols="8"
          sm="4"
          md="2"
        >
     <v-text-field
        v-model="pass"
        :rules="rules.pass"
        outlined
        required
      ></v-text-field>
      </v-col>
      </v-row>
 <label><b><i>GENERATED PASSWORD</i></b></label>
  <v-row>
       <v-col
          cols="12"
          sm="6"
          md="3"
        >
      <v-text-field
        v-model="password"
        readonly
        outlined
      ></v-text-field>
      </v-col>
      </v-row>
<div>
<label for="gender"><b><i>GENDER :</i></b></label>
<div class="space">
  </div>
<input type="radio" id="male" v-model="gender" value="MALE">
<div class="space1">
  </div>
<label for="male">MALE</label>
<div class="space2">
  </div>
<input type="radio" id="female" v-model="gender" value="FEMALE">
<div class="space3">
  </div>
<label for="female">FEMALE</label><br>
</div>
<br>
<div>
  <label for="interest"><b><i>INTEREST :</i></b> </label>
<div class="space4">
  </div>
<input type="checkbox" id="interest1" v-model="interest" value="CRICKET">
<div class="space5">
  </div>
<label for="interest1">CRICKET</label>
<div class="space6">
  </div>
<input type="checkbox" id="interest2" v-model="interest" value="HOCKEY">
<div class="space7">
  </div>
<label for="interest2">HOCKEY</label>
<div class="space8">
  </div>
<input type="checkbox" id="interest3" v-model="interest" value="FOOTBALL">
<div class="space9">
  </div>
<label for="interest3">FOOTBALL</label>
</div>
<br>
 <label for="location"><b><i>LOCATION :</i></b> </label>
<v-row>
      <v-col cols="4">
        <v-combobox
          v-model="location"
          :items="items"
          multiple
          outlined
          dense
        ></v-combobox>
      </v-col>
    </v-row>
<br>

 <v-row
    align="center"
    justify="space-around"
  >
    <v-btn depressed color ="primary" v-on:click="onsubmit()">
      SUBMIT
    </v-btn>
 <v-btn depressed color ="normal" v-on:click="resetInput()">
      CANCEL
    </v-btn>
    </v-row>
</form>
<br>
 <v-simple-table dark>
    <template v-slot:default>
      <thead>
        <tr>
         <th class="text-left">
           ID
          </th>
          <th class="text-left">
            NAME
          </th>
          <th class="text-left">
            EMAIL ID
          </th>
            <th class="text-left">
            GENDER
          </th>
          <th class="text-left">
            INTEREST
          </th>
           <th class="text-left">
            LOCATION
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
        <tr v-for="(item, index) in all" :key="index">
         <th scope="row">{{ index+1 }}</th>
          <td>{{ item.name }}</td>
          <td>{{ item.email }}</td>
           <td>{{ item.gender }}</td>
          <td>{{ item.interest }}</td>
           <td>{{ item.location }}</td>
           <td> <v-btn depressed color ="teal" @click="Update()">
               UPDATE
            </v-btn></td>
            <td> <v-btn depressed color ="error" @click="deleteTableRow(index)">
               DELETE
            </v-btn></td>

        </tr>
      </tbody>
    </template>
  </v-simple-table>



    <HelloWorld />
    </div>
</template>
<script>
  import HelloWorld from '../components/HelloWorld'
  export default {
    name: 'HomeView',

    components: {
      HelloWorld,
    },
    data () {
      return {
        name: '',
        email: '',
        pass:'',
        password:'',
        interest:[],
        gender:'',
        location:[],
        all: [],
        rules: {
          req: [val => (val || '').length > 0 || 'Mandatory Field', val => (!val) || /^[a-zA-Z\s]*$/.test(val) || 'Please type only alphabets'],
          required: value => !!value || 'Required.',
          email: value => {
            const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
            return pattern.test(value) || 'Invalid e-mail. Check again'
          },
          pass: [val => (val|| '').length > 0 || 'Mandatory Field', val => (!val) || /^[0-9]*$/.test(val) || 'oops please check.only numbers', val => (7 < (val)) && ((val) < 21) || 'must be between 8 and 20']

        },
        select: [ ],
        items: [
          'CHENNAI',
          'MUMBAI',
          'KOLKATA',
          'NAGPUR',
          'DELHI',
          'COIMBATURE',
          'HIMACHAL PRADESH',
        ],
  }
    },
 watch:{
    pass(value){
      this.pass = value
      if(value<8 || value>20 || /^[a-zA-Z\s]*$/.test(value)){
        this.password = ''
      }
      else{
        this.randomPassword()
      }
    }
  },
  
  methods:{
    randomPassword(){
      const random = {
        Uppers: "QWERTYUIOPASDFGHJKLZXCVBNM",
        Lowers: "qwertyuiopasdfghjklzxcvbnm",
        Numbers: "1234567890",
        Symbols: "!@#$%^&*"
      }
      const getRandomCharFromString = (str) => str.charAt(Math.floor(Math.random() * str.length))
      const generate = (length = this.pass) => { 
        let ran = "";
        ran += getRandomCharFromString(random.Uppers); 
        ran += getRandomCharFromString(random.Lowers); 
        ran += getRandomCharFromString(random.Numbers); 
        ran += getRandomCharFromString(random.Symbols);
        for (let i = ran.length; i < length; i++)
            ran += getRandomCharFromString(Object.values(random).join('')); 
        return ran
      }
      this.password = generate(this.pass)
    },

   

onsubmit()
{
   this.all.push({ name: this.name, email: this.email, gender: this.gender, interest: this.interest, location: this.location });
   console.log(this.all);
},
deleteTableRow(index) { 
  console.log(index)
      this.all.splice(index, 1);      
   },

 resetInput() {
      this.name = "";
      this.email = "";
      this.pass = "";
      this.password = "";  
    },

  }
  }
</script>
<style scoped>
.space{
  width: 13px;
  height: auto;
  display: inline-block;

}
.space1{
  width: 13px;
  height: auto;
  display: inline-block;

}
.space2{
  width: 13px;
  height: auto;
  display: inline-block;

}
.space3{
  width: 13px;
  height: auto;
  display: inline-block;

}
.space4{
  width: 8px;
  height: auto;
  display: inline-block;

}
.space5{
  width: 13px;
  height: auto;
  display: inline-block;

}
.space6{
  width: 13px;
  height: auto;
  display: inline-block;

}
.space7{
  width: 13px;
  height: auto;
  display: inline-block;

}
.space8{
  width: 13px;
  height: auto;
  display: inline-block;

}
.space9{
  width: 13px;
  height: auto;
  display: inline-block;

}

</style>
