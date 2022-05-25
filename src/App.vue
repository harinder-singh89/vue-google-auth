<template>
  <div id="app">
    <Login
      @auth="auth"
      ref="refobj"
      @SignOutFailure="SignOutFailure"
      @status="getstatus"
      @SignInsuccess="Signin"
      @SignOutSuccess="SignOutSuccess"
      @SigninFailed="SigninFailed"
      :clientId="clientId"
    />
  </div>
</template>

<script>
import Login from './components/Login.vue'

export default {
  name: 'App',
  components: {
    Login
  },
  data(){
    return{
      clientId: "GOOGLE_CLIENT_ID",
    }
  },
  methods:{
    SigninFailed(error){
      console.log("SigninFailed",error)
    },
    getstatus(status){
      console.log("Signed in Staus",status);
    },
    Signin(user){
      //signin success 
      console.log("signin Success",user);
    },
    SignOutSuccess(){
      //signout success
      console.log("SignOutSuccess");
    },
    SignOutFailure(){
      //signout failure
      console.log("SignOutFailure");

    },
    auth(auth){
      // you can store the auth object and directly use the auth instance to sign in or signor signout
     auth.signIn()
          .then((user) => {
            this.user = user.getBasicProfile();
          })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
