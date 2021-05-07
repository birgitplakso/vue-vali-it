<template>
  <div class="home">
    <input v-model="email" placeholder="enter your email">
    <button v-on:click="register()">Register</button>
    <table border="1">
      <tr v-for="email in emails"> <!--tr on rida, nii mitu rida kui mitu emaili on sisestatud -->
        <td>{{email}}</td>  <!--td on tulp -->
      </tr>
    </table>
  </div>
</template>

<script>

export default{
  data:function (){
    return{
      'email': '',
      'emails':['','']
    }
  },
  methods: {
    'register': function(){
      this.emails.push(this.email);
      //alert(this.email);
    }
  }
}


</script>
