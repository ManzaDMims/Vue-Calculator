<!-- File: src/components/Calculator.vue -->

<template>
  <div class="calculator">
    <div class="display">{{ current }}</div>
    <div class="buttons">
      <button @click="clear">C</button>
      <button @click="append('/')">/</button>
      <button @click="append('*')">*</button>
      <button @click="append('-')">-</button>
      <button @click="append('7')">7</button>
      <button @click="append('8')">8</button>
      <button @click="append('9')">9</button>
      <button @click="append('+')">+</button>
      <button @click="append('4')">4</button>
      <button @click="append('5')">5</button>
      <button @click="append('6')">6</button>
      <button @click="calculate">=</button>
      <button @click="append('1')">1</button>
      <button @click="append('2')">2</button>
      <button @click="append('3')">3</button>
      <button @click="append('0')">0</button>
      <button @click="append('.')">.</button>
    </div>
    <div class="history">
      <h3>History</h3>
      <ul>
        <li v-for="(entry, index) in history" :key="index">{{ entry }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      current: '',
      history: [],
    };
  },
  methods: {
    append(char) {
      this.current += char;
    },
    clear() {
      this.current = '';
    },
    calculate() {
      try {
        const result = eval(this.current);
        this.history.unshift(`${this.current} = ${result}`);
        this.current = result.toString();
      } catch (e) {
        this.current = 'Error';
      }
    },
  },
};
</script>

<style>
.calculator {
  display: inline-block;
  padding: 10px;
  border: 2px solid #000;
  border-radius: 5px;
}
.display {
  margin-bottom: 10px;
  padding: 10px;
  background: #000;
  color: #fff;
  text-align: right;
  font-size: 2em;
  border-radius: 5px;
}
.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}
button {
  padding: 20px;
  font-size: 1.5em;
  cursor: pointer;
  border: none;
  border-radius: 5px;
  background: #f0f0f0;
}
button:active {
  background: #ddd;
}
.history {
  margin-top: 20px;
}
.history h3 {
  margin: 0;
}
.history ul {
  padding: 0;
  list-style: none;
}
.history li {
  text-align: left;
}
</style>