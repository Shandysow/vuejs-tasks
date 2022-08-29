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
                              label="User Name"
                           ></v-text-field>
                           <v-text-field
                              id="email"
                              name="email"
                              v-model="email"
                              label="Email"
                           ></v-text-field>
                                <v-text-field
                              name="Password"
                              label="Password"
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