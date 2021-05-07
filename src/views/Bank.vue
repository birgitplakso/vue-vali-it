<template>
  <div class="home">
    <h1> Welcome to the Bank of Estonia</h1>
    <h3>Create bank account </h3>
    <input v-model="customerName" placeholder="enter your name">
    <input v-model="accountNr" placeholder="enter your account number">
    <input v-model="initialBalance" placeholder="enter the amount">
    <button v-on:click="createAccount()">Create Account</button>
    {{newAccResponse}}
    <br>
    <br>

    <h3>Get balance </h3>
    <input v-model="accountNrBalance" placeholder="enter your account number">
    <button v-on:click="getAccountBalance()">Get Balance</button>
    {{accBalance}}
    <br>
    <br>

    <h3>Block account</h3>
    <input v-model="accountNrBlock" placeholder="enter your account number">
    <button v-on:click="blockAccount()">Block</button>
    {{blockResponse}}
    <br>
    <br>

    <h3>Unblock account</h3>
    <input v-model="accountNrUnBlock" placeholder="enter your account number">
    <button v-on:click="unBlockAccount()">Unblock</button>
    {{unBlockResponse}}
    <br>
    <br>

    <h3>Deposit money </h3>
    <input v-model="accountNrDeposit" placeholder="enter your account number">
    <input v-model="depositAmount" placeholder="enter the amount">
    <button v-on:click="depositMoney()">Deposit</button>
    {{depositResponse}}
    <br>
    <br>

    <h3>Withdraw money </h3>
    <input v-model="accountNrWithdraw" placeholder="enter your account number">
    <input v-model="withdrawAmount" placeholder="enter the amount">
    <button v-on:click="withdrawMoney()">Withdraw</button>
    {{withdrawResponse}}
    <br>
    <br>

    <h3>Transfer money </h3>
    <input v-model="firstAccNr" placeholder="enter account number (from)">
    <input v-model="secondAccNr" placeholder="enter account number (to)">
    <input v-model="transferAmount" placeholder="enter the amount">
    <button v-on:click="transferMoney()">Transfer</button>
    {{transferResponse}}
    <br>
    <br>



    <h3>Get list of accounts </h3>
    <button v-on:click="getListOfAccounts()">Get accounts</button>
    <br>
    <br>
    <table border="1" style="width:60%" align="center">
      <tr>
        <th> Customer name</th>
        <th> Account Number </th>
        <th> Balance </th>
        <th> Is blocked </th>
      </tr>
      <tr v-for="account in accList">
        <td>{{ account.ownerName }}</td>
        <td>{{ account.accountNumber }}</td>
        <td>{{ account.amount }}</td>
        <td>{{ account.blocked }}</td>
      </tr>
    </table>
    <br>
    <br>

    <h3>Get list of transactions </h3> <!-- kasuta fn'is mounted(fn järel, sulgudest väljas) kui tahan et lehele minnes kuvatakse
    koheselt mingi teenus/meetodi tulemus (a la eraldi lehel on transaction list)-->
    <input v-model="accNrTransactions" placeholder="enter your account number">
    <button v-on:click="getListOfTransactions()">Get transactions</button>
    <br>
    <br>
    <table border="1" style="width:60%" align="center">
      <tr>
        <th> Account number </th>
        <th> Account Balance </th>
        <th> Transfer time </th>
      </tr>
      <tr v-for="transaction in transactionList">
        <td>{{ transaction.accountNumber }}</td>
        <td>{{ transaction.accountBalance }}</td>
        <td>{{ transaction.transferTime }}</td>
      </tr>
    </table>
    <br>
    <br>



  </div>
</template>

<script>

export default{
  data:function (){
    return{
      'customerName': '',
      'accountNr': '',
      'initialBalance': '',
      'newAccResponse': '',
      'accountNrBalance': '',
      'accBalance': '',
      'accountNrBlock': '',
      'blockResponse': '',
      'accountNrUnBlock': '',
      'unBlockResponse': '',
      'accountNrDeposit': '',
      'depositAmount': '',
      'depositResponse': '',
      'accountNrWithdraw': '',
      'withdrawAmount': '',
      'withdrawResponse': '',
      'firstAccNr': '',
      'secondAccNr': '',
      'transferAmount': '',
      'transferResponse': '',
      'accList': [],
      'accNrTransactions': '',
      'transactionList': ''
    }
  },
  methods: {
    'getAccountBalance': function () {
      this.$http.get('api/getAccountBalance/' + this.accountNrBalance)
          .then(response => {
            console.log(response);
            this.accBalance = response.data

          })
          .catch(response => {
            alert('juhtus viga')
          })
    },
    'createAccount': function(){
      this.$http.post('api/createBankAccount',{
        ownerName: this.customerName,
        accountNumber: this.accountNr,
        amount: this.initialBalance

          })
          .then(response => {
            console.log(response);
            this.newAccResponse = response.data
          })
          .catch(response => {
            alert('juhtus viga')
          })
    },
    'blockAccount': function (){
      this.$http.put('api/blockAccount', {
        accountNumber: this.accountNrBlock
      })
      .then(response => {
        console.log(response);
        this.blockResponse = response.data
      })
          .catch(response => {
            alert('juhtus viga')
          })
    },
    'unBlockAccount': function (){
      this.$http.put('api/unBlockAccount', {
        accountNumber: this.accountNrUnBlock
      })
          .then(response => {
            console.log(response);
            this.unBlockResponse = response.data
          })
          .catch(response => {
            alert('juhtus viga')
          })
    },
    'depositMoney': function (){
      this.$http.put('api/deposit', {
        accountNumber: this.accountNrDeposit,
        amount: this.depositAmount
      })
          .then(response => {
            console.log(response);
            this.depositResponse = response.data
          })
          .catch(response => {
            alert('juhtus viga')
          })
    },
    'withdrawMoney': function (){
      this.$http.put('api/withdraw', {
        accountNumber: this.accountNrWithdraw,
        amount: this.withdrawAmount
      })
          .then(response => {
            console.log(response);
            this.withdrawResponse = response.data
          })
          .catch(response => {
            alert('juhtus viga')
          })
    },
  'transferMoney': function(){
    this.$http.put('api/transferMoney/'+this.firstAccNr,{
      accountNumber: this.secondAccNr,
      amount: this.transferAmount
    })
        .then(response => {
          console.log(response);
          this.transferResponse = response.data
        })
        .catch(response => {
          alert('juhtus viga')
        })
  },
    'getListOfAccounts': function (){
      this.$http.get('api/accountList')
      .then(response=> {
        console.log(response);
        this.accList=response.data
      })
      .catch(response=>{
        alert('juhtus viga')
      })
    },
    'getListOfTransactions': function (){
      this.$http.get('api/listOfTransactions/'+this.accNrTransactions)
          .then(response=> {
            console.log(response);
            this.transactionList=response.data
          })
          .catch(response=>{
            alert('juhtus viga')
          })
    }
  }
}


</script>
