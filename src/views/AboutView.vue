<template>
  <div>
  <v-app id="inspire">
      <v-content>
         <v-container fluid fill-height>
            <v-layout align-center justify-center>
               <v-flex xs12 sm8 md4>
                  <v-card class="elevation-12">
                     <v-toolbar dark color="black">
                        <v-toolbar-title>LOGIN PAGE</v-toolbar-title>
                     </v-toolbar>
                     <v-card-text>
                        <v-form>
                           <v-text-field
                              name="username"
                              v-model="username"
                              :rules="[rules.required]"
                              label="User Name"
                           ></v-text-field>
                           <v-text-field
                              id="email"
                              name="email"
                              v-model="email"
                              :rules="[rules.required]"
                              label="Email"
                           ></v-text-field>
                                <v-text-field
                              name="Password"
                              label="Password"
                              :rules="[rules.required]"
                              v-model="password"
                              type="password"
                           ></v-text-field>
                        </v-form>
                     </v-card-text>
                     <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn color="primary" v-on:click="login()">login </v-btn>
                     </v-card-actions>
                  </v-card>
               </v-flex>
            </v-layout>
         </v-container>
      </v-content>
   </v-app>
  </div>
</template>
<script>

export default {
name:'loginPage',
data(){

    return{
        username:'',
        email:'',
        password:'',
        errors:[],
         rules: {
            required:'Required',
      //       email: value => {
      //       const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
      //       return pattern.test(value) || 'Invalid e-mail. Check again'
      //     },
      //     pass: value =>{
      //     const pattern1 =/^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
      //      return pattern1.test(value) || 'Min.8 characters with at least one capital letter, a number and a special character.'
      //   },      
       
       }
}
},
methods:{
      login() {
        if (this.email == 'Test123#@gmail.com' && this.username == 'sowmya' && this.password == 'abc123') {
          this.$router.push('/home');
          alert('login successful !!')
        } else {
          this.$router.push('/');
          alert('login failed !!')
        }
        localStorage.setItem("loggedin",JSON.stringify(this.username))

},
}
}

</script>