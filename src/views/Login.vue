<template>
  <div class="home">
    <h1>Login to access Bank services</h1>
    <br>
    <h3>Provide data to sign in: </h3>
    <input v-model="username" placeholder="username">
    <input v-model="password" placeholder="password">
    <button v-on:click="login()">Login</button>
    {{loginResponse}}
    <br>
    <br>
    <h3>Enter data to create new user: </h3>
    <input v-model="usernameNew" placeholder="username">
    <input v-model="passwordNew" placeholder="password">
    <button v-on:click="createUser()">Create new user</button>
    {{createUserResponse}}
    <br>
    <br>
    <h5>To logout : </h5>
    <button v-on:click="logout()">Logout</button>
    {{logoutResponse}}
  </div>
</template>

<script>

export default {
  data: function () {
    return {
      'username': '',
      'password': '',
      'loginResponse': '',
      'usernameNew': '',
      'passwordNew': '',
      'createUserResponse': '',
      'logoutResponse': ''
    }
  },
  methods: {
    'login': function () {
      this.$http.put('api/public/login', {
        username: this.username,
        password: this.password
      })
          .then(response => {

            console.log(response);
            let token = response.data
            localStorage.setItem('user-token',token)
            this.$http.defaults.headers.common['Authorization']="Bearer "+token
            this.loginResponse=" You are logged in"
          })
          .catch(response => {
            alert('juhtus viga')
          })
    },
    'logout': function (){
      localStorage.removeItem('user-token')
      location.reload()
      this.logoutResponse=" You are logged out"

    },
    'createUser': function () {
      this.$http.post('api/public/createUser', {
        username: this.usernameNew,
        password: this.passwordNew
      })
          .then(response => {
            console.log(response);
            this.createUserResponse = response.data
          })
          .catch(response => {
            alert('juhtus viga')
          })
    }
  }
}
</script>
