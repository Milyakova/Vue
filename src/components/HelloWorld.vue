<template>
  <div class="hello">
    <h1>{{ message }}</h1>
    <!--
      1-Change data
      2-Update data
    -->
    <!-- <input type="text" :value="message" @input="changeInput($event)"/>
    <button @click="someMethodClick" v-bind:disabled="disabled">Click</button> -->
    <input type="text" v-model.number="operand1" />
    <input type="text" v-model.number="operand2" />

    = {{ result }}
    <button @click="clean">Сбросить</button>
    <hr />
    <button @click="result = operand1 + operand2">+</button>
    <button @click="result = operand1 - operand2">-</button>
    <button @click="divide">/</button>
    <button @click="multiply(operand1, operand2)">*</button>
    <button @click="square(operand1, operand2)">**</button>
    <button @click="trunc(operand1, operand2)">Целочисленное деление</button>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      disabled: true,
      message: "",
      operand1: 0,
      operand2: 0,
      result: 0,
    };
  },
  methods: {
    divide() {
      this.result = this.operand1 / this.operand2;
    },
    multiply(op1, op2) {
      this.result = op1 * op2;
    },
    square(op1, op2) {
      this.result = op1 ** op2;
    },
    trunc(op1, op2) {
      this.result = Math.trunc(op1 / op2);
    },
    clean() {
      this.operand1 = 0;
      this.result = 0;
      this.operand2 = 0;
    },
    changeInput(event) {
      this.message = event.target.value;
      console.log(event);
    },
    someMethodClick(event) {
      console.log("click", event);
    },
    someMethodKeyUp() {
      console.log("keyup");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
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
</style>
