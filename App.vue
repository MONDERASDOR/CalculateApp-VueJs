<template>
  <div>
    <h1>Simple Calculator</h1>
    <input type="text" v-model="display" readonly />
    <div>
      <button @click="appendNumber('1')">1</button>
      <button @click="appendNumber('2')">2</button>
      <button @click="appendNumber('3')">3</button>
      <button @click="setOperation('+')">+</button>
      <button @click="clear">C</button>
      <button @click="calculate">=</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      display: '',
      operator: null,
      operand: null,
    };
  },
  methods: {
    appendNumber(number) {
      this.display += number;
    },
    setOperation(op) {
      this.operand = parseFloat(this.display);
      this.display = '';
      this.operator = op;
    },
    calculate() {
      if (this.operator === '+') {
        this.display = (this.operand + parseFloat(this.display)).toString();
      }
    },
    clear() {
      this.display = '';
      this.operator = null;
      this.operand = null;
    },
  },
};
</script>
