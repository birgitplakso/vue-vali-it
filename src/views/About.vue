<template>
  <div class="about">
    <h1>Min</h1>
    <input v-model.number="minA">
    <input v-model.number="minB">
    <button v-on:click="min()">Min</button>
    {{minAnswer}}

    <h1>Max</h1>
    <input v-model.number="maxA">
    <input v-model.number="maxB">
    <button v-on:click="max()">Max</button>
    {{maxAnswer}}

    <h1>Abs</h1>
    <input v-model.number="absA">
    <button v-on:click="abs()">Abs</button>
    {{absAnswer}}

    <h1>Is even?</h1>
    <input v-model.number="evenA">
    <button v-on:click="isEven()">isEven</button>
    {{evenAnswer}}

    <h1>Min3</h1>
    <input v-model.number="min3A">
    <input v-model.number="min3B">
    <input v-model.number="min3C">
    <button v-on:click="min3()">Min3</button>
    {{min3Answer}}

    <h1>Max3</h1>
    <input v-model.number="max3A">
    <input v-model.number="max3B">
    <input v-model.number="max3C">
    <button v-on:click="max3()">Max3</button>
    {{max3Answer}}

    <h1>Multiply Table</h1>
    <input v-model.number="x">
    <input v-model.number="y">
    <button v-on:click="show()">OK</button>

    <table border="1">
      <tr v-for="row in table"> <!--tr on rida -->
        <td v-for="column in row">{{column}}</td>  <!--td on tulp -->
      </tr>
    </table>

  </div>
</template>

<script>

function min(){
  if(this.minA<this.minB){
    this.minAnswer=this.minA;
  }else{
    this.minAnswer=this.minB;
  }
}

function max(){
  if(this.maxA>this.maxB){
    this.maxAnswer=this.maxA;
  }else{
    this.maxAnswer=this.maxB;
  }
}

function abs(){
  if(this.absA>0){
    this.absAnswer=this.absA
  }else{
    this.absAnswer=-1*this.absA
  }
}

function isEven(){
  this.evenAnswer=(this.evenA%2==0)

}

function min3() {
  if (this.min3A <= this.min3B && this.min3A <= this.min3C) {
    this.min3Answer=this.min3A
  }
  else if (this.min3B <= this.min3A && this.min3B <= this.min3C) {
    this.min3Answer=this.min3B
  } else {
    this.min3Answer=this.min3C
  }
}

function max3() {
  if (this.max3A >= this.max3B && this.max3A >= this.max3C) {
    this.max3Answer=this.max3A
  }
  else if (this.max3B >= this.max3A && this.max3B >= this.max3C) {
    this.max3Answer=this.max3B
  } else {
    this.max3Answer=this.max3C
  }
}




export default {
  data: function (){
    return{
      'minA': undefined,
      'minB': undefined,
      'minAnswer': undefined,
      'maxA': undefined,
      'maxB': undefined,
      'maxAnswer': undefined,
      'absA': undefined,
      'absAnswer': undefined,
      'evenA':undefined,
      'evenAnswer': undefined,
      'min3A': undefined,
      'min3B': undefined,
      'min3C': undefined,
      'min3Answer': undefined,
      'max3A': undefined,
      'max3B': undefined,
      'max3C': undefined,
      'max3Answer': undefined,
      'x': 0,
      'y': 0,
      'table':[[]]
    }
  },
  methods:{
    'min':min,
    'max':max,
    'abs':abs,
    'isEven':isEven,
    'min3':min3,
    'max3':max3,
    'show':function() {
      for(let i=0; i<this.x; i++){
        this.table[i]=[] //pean tekitama tühja ruudu tabelisse[0], Vue omapära

        for(let j=0; j<this.y; j++){
          this.table[i][j] = (i + 1) * (j + 1);

        }
      }
      this.table.splice(); //ilma selleta tabelit ei teki!!
    }
  }
}
</script>
