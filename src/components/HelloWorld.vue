<template>
<h1 style="color:blue"><b>ARITHMETIC OPERATIONS</b></h1>
 <label><b>Enter number 1 : </b></label>
 <input type="number" v-model="num1"><br><br>
 <label><b>Enter number 2 : </b></label>
  <input type="number" v-model="num2"><br><br>

  <div>
  <button @click="add()"> Add </button>
  <div class="space">
  </div>
 <button v-if="sum >=0" value="sum" class="btn1">SUM IS POSITIVE NUM: {{sum}}
  </button>
  <button v-else class="btn" value="sum">SUM IS NEGATIVE NUMBER: {{sum}}
  </button>
  
 </div>

<br>

<div>
<button @click="sub()"> Sub </button>
 <div class="space1">
</div>
  <button v-if="diff >=0" value="diff" class="btn2">DIFF IS POSITIVE NUM: {{diff}}
  </button>
  <button v-else class="btn3" value="diff">DIFF IS NEGATIVE NUM: {{diff}}
  </button>

 </div>

 <br>

<div>
<button @click="multiply()"> Mul </button>
 <div class="space2">
</div>
  <button v-if="mul >=0" value="mul" class="btn4">PRODUCT IS POSITVE : {{mul}}
  </button>
  <button v-else class="btn5" value="mul">PRODUCT IS NEGATIVE: {{mul}}
  </button>
</div>
<br>

<div>
<button @click="division()"> Quot </button>
 <div class="space3">
</div>
  <button v-if="div >=0" value="div" class="btn6">DIVISION IS POSITIVE: {{div}}
  </button>
  <button v-else class="btn7" value="div">DIVISION IS NEGATIVE: {{div}}
  </button><br><br>

   <button @click="resetInput()"> Reset
  </button>
 </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
 data(){
  return{
  num1: 0,
  num2: 0,
  sum:0,
  diff:0,
  mul:0,
  div:0
 }
 },
 methods:{
 add() {
 this.sum = parseInt(this.num1)+parseInt(this.num2);
 console.log(this.sum)
},

sub() {
 this.diff = parseInt(this.num1)-parseInt(this.num2);
 console.log(this.diff)
},

multiply() {
 this.mul = parseInt(this.num1)*parseInt(this.num2)
 console.log(this.mul)
},
division() {
 this.div = parseInt(this.num1)/parseInt(this.num2);
 console.log(this.div)
},
resetInput() {
      this.sum = 0;
      this.diff = 0;
      this.mul = 0;
      this.div = 0;   
       },
 }
 }

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.btn1
{
  background-color: lightgreen;
}
.btn
{
  background-color: red;
}
.btn2
{
  background-color: lightgreen;
}
.btn3
{
  background-color: red;
}

.btn4
{
  background-color: lightgreen;
}
.btn5
{
  background-color: red;
}

.btn6
{
  background-color: lightgreen;
}
.btn7
{
  background-color: red;
}

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


</style>
