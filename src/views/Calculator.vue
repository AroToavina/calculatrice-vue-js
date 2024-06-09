<template>
  <body>
    <div class="calculator">
      <div class="display">
        {{ current || 'Enter a number' }}
      </div>
      <div class="buttons">
        <button @click="clear" class="main">C</button>
        <button @click="del" class="main">del</button>
        <button @click="append('-')" class="main">+/-</button>
        <button @click="setOperator('divide')" class="operator">/</button>
        <button @click="append('7')">7</button>
        <button @click="append('8')">8</button>
        <button @click="append('9')">9</button>
        <button @click="setOperator('multiply')" class="operator">x</button>
        <button @click="append('4')">4</button>
        <button @click="append('5')">5</button>
        <button @click="append('6')">6</button>
        <button @click="setOperator('subtract')" class="operator">-</button>
        <button @click="append('1')">1</button>
        <button @click="append('2')">2</button>
        <button @click="append('3')">3</button>
        <button @click="setOperator('add')" class="operator">+</button>
        <button @click="append('0')" class="wide">0</button>
        <button @click="dot">.</button>
        <button @click="equal" class="operator">=</button>
      </div>
    </div>
  </body>
</template>
  
  <script>
  export default {
    data() {
      return {
        current: '',
        previous: null,
        operator: null,
        operatorClicked: false
      };
    },
    methods: {
      clear() {
        this.current = '';
      },
      del() {
        this.current = this.current.toString().slice(0, -1);
      },
      append(number) {
        if (this.operatorClicked) {
          this.current = '';
          this.operatorClicked = false;
        }
        this.current = `${this.current}${number}`;
      },
      dot() {
        if (this.current.indexOf('.') === -1) {
          this.append('.');
        }
      },
      setOperator(op) {
        if (this.current && this.previous) {
          this.equal();
        }
        this.operator = op;
        this.previous = this.current;
        this.current = '';
        this.operatorClicked = true;
      },
      equal() {
        const prev = parseFloat(this.previous);
        const current = parseFloat(this.current);
        if (this.operator === 'add') {
          this.current = prev + current;
        } else if (this.operator === 'subtract') {
          this.current = prev - current;
        } else if (this.operator === 'multiply') {
          this.current = prev * current;
        } else if (this.operator === 'divide') {
          this.current = prev / current;
        }
        this.previous = null;
        this.operator = null;
      }
    }
  };
  </script>
  
  <style scoped>
  .calculator {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-size: 48px;
  }
  
  .display {
    margin-bottom: 20px;
    border-radius: 20px;
    width: 320px;
    overflow: hidden;
    text-align: right;
    overflow-x: auto;
}

  .main {
    background-color: rgb(184, 184, 184);
  }

  .main:hover {
    background-color: rgb(59, 59, 59);
    color: white;
  }

  .operator {
    color: white;
    background-color: orange;
  }

  .operator:hover {
    background-color: rgb(238, 170, 43);
  }
  
  .buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
  }
  
  button {
    background-color: grey;
    border: none;
    font-size: 24px;
    padding: 20px;
    cursor: pointer;
    border-radius: 50%;
    color: white;
  }
  
  button:hover {
    background-color: rgb(206, 206, 206);
    color: black;
  }

  .wide {
    grid-column: span 2;
    border-radius: 20px;
  }
  </style>
  