<template>
  <div class="flex justify-center items-center h-screen bg-gray-100">
    <div class="bg-white shadow-lg rounded-lg p-6 max-w-xs w-full">
      <h1 class="text-2xl font-bold text-center mb-4">Simple Calculator</h1>

      <input
        type="text"
        v-model="display"
        readonly
        class="w-full text-right p-3 bg-gray-200 rounded mb-4 text-xl font-mono"
      />

      <div class="grid grid-cols-4 gap-2">
        <!-- Row 1 -->
        <button @click="appendNumber('1')" class="btn">1</button>
        <button @click="appendNumber('2')" class="btn">2</button>
        <button @click="appendNumber('3')" class="btn">3</button>
        <button @click="setOperation('+')" class="btn-operator">+</button>

        <!-- Row 2 -->
        <button @click="appendNumber('4')" class="btn">4</button>
        <button @click="appendNumber('5')" class="btn">5</button>
        <button @click="appendNumber('6')" class="btn">6</button>
        <button @click="setOperation('-')" class="btn-operator">-</button>

        <!-- Row 3 -->
        <button @click="appendNumber('7')" class="btn">7</button>
        <button @click="appendNumber('8')" class="btn">8</button>
        <button @click="appendNumber('9')" class="btn">9</button>
        <button @click="setOperation('*')" class="btn-operator">×</button>

        <!-- Row 4 -->
        <button @click="clear" class="btn-clear">C</button>
        <button @click="appendNumber('0')" class="btn">0</button>
        <button @click="calculate" class="btn-equal">=</button>
        <button @click="setOperation('/')" class="btn-operator">÷</button>
      </div>
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
      let result;
      const current = parseFloat(this.display);

      if (isNaN(this.operand) || isNaN(current)) return;

      switch (this.operator) {
        case '+':
          result = this.operand + current;
          break;
        case '-':
          result = this.operand - current;
          break;
        case '*':
          result = this.operand * current;
          break;
        case '/':
          result = this.operand / current;
          break;
        default:
          return;
      }

      this.display = result.toString();
      this.operator = null;
      this.operand = null;
    },
    clear() {
      this.display = '';
      this.operator = null;
      this.operand = null;
    },
  },
};
</script>

<style scoped>
.btn {
  @apply bg-blue-500 text-white p-3 rounded font-bold hover:bg-blue-600 transition duration-200;
}

.btn-operator {
  @apply bg-yellow-500 text-white p-3 rounded font-bold hover:bg-yellow-600 transition duration-200;
}

.btn-clear {
  @apply bg-red-500 text-white p-3 rounded font-bold hover:bg-red-600 transition duration-200;
}

.btn-equal {
  @apply bg-green-500 text-white p-3 rounded font-bold hover:bg-green-600 transition duration-200;
}
</style>
