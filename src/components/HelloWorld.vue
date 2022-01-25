<template>
  <div class="hello">
    <h1>{{ message }}</h1>
    <!-- <input type="text" :value="message" @input="changeInput($event)"/>
    <button @click="someMethodClick" v-bind:disabled="disabled">Click</button> -->
    <input type="text" v-model="operand1" />
    <input type="text" v-model="operand2" />
    = {{ result }}<br />

    {{ error }}

    <button
      v-for="(operand, idx) in operands"
      :key="idx"
      @click="calculate(operand)"
    >
      {{ operand }}</button
    ><br />

    <input type="checkbox" id="checkbox" v-model="screenKeyboard" />
    <label for="checkbox">Отобразить экранную клавиатуру</label>

    <div v-if="screenKeyboard">
      <button
        v-for="(keyButton, idx) in myCollection"
        :key="idx"
        @click="enterKeys(keyButton)"
      >
        {{ keyButton }}
      </button>
      <br />
      <input
        type="radio"
        id="operand1"
        value="operand1"
        name="radioOperand"
        v-model="pickedOperand"
      />
      <label for="operand1">Операнд 1</label>
      <input
        type="radio"
        id="operand2"
        value="operand2"
        name="radioOperand"
        v-model="pickedOperand"
      />
      <label for="operand2">Операнд 2</label>
    </div>
    {{ logs }}
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
      error: "",
      myCollection: [1, 2, 3, 4, 5, 6, 7, 8, 9, "backspace"],
      operands: ["+", "-", "/", "*"],
      screenKeyboard: true,
      pickedOperand: "operand1",
      logs: {},
    };
  },

  methods: {
    calculate(operation = "+") {
      this.error = "";
      switch (operation) {
        case "+":
          this.add();
          break;
        case "-":
          this.subsctract();
          break;
        case "*":
          this.multiply();
          break;
        case "/":
          this.divide();
          break;
        case "**":
          this.square();
          break;
        case "trunc":
          this.trunc();
          break;
        default:
          break;
      }
      const key = Date.now();
      const value = `${this.operand1}${operation}${this.operand2} = ${this.result}`;
      this.$set(this.logs, key, value);
    },
    add() {
      this.result = this.operand1 + this.operand2;
    },
    subsctract() {
      this.result = this.operand1 - this.operand2;
    },
    divide() {
      const { operand1, operand2 } = this;
      if (operand2 === 0) {
        this.error = "На 0 делить нельзя";
        return;
      }
      this.result = operand1 / operand2;
    },
    multiply() {
      this.result = this.operand1 * this.operand2;
    },
    square() {
      this.result = this.operand1 ** this.operand2;
    },
    trunc() {
      this.result = Math.trunc(this.operand1 / this.operand2);
    },

    enterKeys(keyButton) {
      if (keyButton === "backspace") {
        keyButton = "";
      }
      if (this.pickedOperand === "operand1") {
        this.operand1 = keyButton;
      } else {
        this.operand2 = keyButton;
      }
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
