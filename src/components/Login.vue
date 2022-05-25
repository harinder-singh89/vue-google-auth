<template>
  <div>
    <button @click="signin" :class="`g-signin-button ${userDefinedClass}`">
      {{ status ? signoutText : signinText }}
    </button> 
  </div>
</template>

<script>
export default {
  data() {
    return {
      status: false,
      auth2: "",
    };
  },
  props:{
    userDefinedClass:{
        type: Object,
        default: () => ({})
    },
    signinText:{
      default:'Sign In'
    },
    signoutText:{
      default:'Sign Out'
      
    },
    clientId:{
      required:true
    }
  },
  mounted() {
    if (!window.gapi) {
      throw new Error(
        '"https://apis.google.com/js/api:client.js" needs to be included as a <script>.'
      );
    } else {
      window.gapi.load("auth2", () => {
        this.auth2 = window.gapi.auth2.init({
          client_id: this.clientId,
          scope: "email profile",
          fetch_basic_profile: true,
        });
        this.getstatus();
        this.$emit('auth', this.auth2);
     });
    }

    if (!this.clientId) {
      throw new Error("Client Id must be specified.");
    }
  },
  methods: {
    getstatus() {
      this.status = this.auth2.isSignedIn.get();
      this.$emit('status',this.status);
},
    signin() {
      if (!this.status) {
        this.auth2
          .signIn()
          .then((user) => {
            this.getstatus();
            let userProfile = user.getBasicProfile();
            let profile = {
              name: userProfile.getName(),
              email: userProfile.getEmail(),
              url: userProfile.getImageUrl(),
              id: userProfile.getId(),
            };
            this.$emit('SignInsuccess', profile);
          })
          .catch((error) => {
            this.$emit('SigninFailed', error);

          });
      } else {
        this.auth2.signOut().then(() => {
            this.$emit('SignOutSuccess');
          this.getstatus();
        }).catch((error)=>{
            this.$emit('SignOutFailure', error);

        });
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.g-signin-button {
  box-sizing: border-box;
  position: relative;
  /* width: 13em;  - apply for fixed size */
  margin: 0.2em;
  padding: 0 15px 0 46px;
  border: none;
  text-align: left;
  line-height: 34px;
  white-space: nowrap;
  border-radius: 0.2em;
  font-size: 16px;
  color: #fff;
  background: #bb3f30;
}
.g-signin-button:before {
  content: "";
  box-sizing: border-box;
  position: absolute;
  top: 0;
  left: 0;
  width: 34px;
  height: 100%;

  border-right: #bb3f30 1px solid;

  background: url("https://s3-us-west-2.amazonaws.com/s.cdpn.io/14082/icon_google.png")
    6px 6px no-repeat;
}

.g-signin-button:hover,
.g-signin-button:focus {
  cursor: pointer;
  background: #FF3f10;
}

</style>
