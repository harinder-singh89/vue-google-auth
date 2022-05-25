# demo
you can use the component in this way
```
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
```
    refs 
    
    ref object is used to create a refernce to login component instance and access its methods. 
    you can use it as this.$refs.refobj.methodname();
    


    emitted methods 

    @SignOutFailure will be emitted when sign out from the project failed it will return an error as well  
    
    @status method will return you booolean value based on wether you are currently signed in or not.
      
    @SignInsuccess will return the profle object which will contain four value id,name,email and image url
      
    @SignOutSuccess method will be firec when you successfullu logged out
      
    @SigninFailed  will be emitted when sign infailed it will return an error as well  
    
      
    @auth will return an instance of gapi you can use it to call the signin methods directly.

    
    
    Props 
    
    clientId is a required prop you need to provide a client id to integrate your google signin.

    userDefinedClass prop can be used to provide a custom css class as per your need
     
    signinText prop  can be used  to provide the text on signin button
    
    signoutText  prop  can be used to provide the text on signout button

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
