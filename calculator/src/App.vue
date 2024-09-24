<template>
  <div id="app">
    <h2 id="heading">Simple Calculator</h2>
    <div class="calculator">
      <input type="text" class="result"
               :value="result" readonly />
      <div class="buttons">
        <button class="num" 
                @click="handleClick('7')">7</button>
        <button class="num"
                @click="handleClick('8')">8</button>
        <button class="num"
                @click="handleClick('9')">9</button>
       
        <button class="num"
                @click="handleClick('4')">4</button>
        <button class="num" 
                @click="handleClick('5')">5</button>
        <button class="num"
                @click="handleClick('6')">6</button>
        

        <button class="num"
                @click="handleClick('1')">1</button>
        <button class="num"
                @click="handleClick('2')">2</button>
        <button class="num" 
                @click="handleClick('3')">3</button>


        <button class="num"
                @click="handleClick('0')">0</button>
        <button class="num"
                @click="handleClick('.')">.</button>
        <button class="operator"
                @click="handleOperatorClick('/')">/</button>


        <button class="operator"
                @click="handleOperatorClick('*')">x</button>
        <button class="operator"
                @click="handleOperatorClick('-')">-</button>
        <!-- <button class="number" 
                @click="handleClick('00')">00</button> -->
        <button class="operator" 
                @click="handleOperatorClick('+')">+</button>

        <button class="clear"
                @click="handleClear">CA</button>
        <button class="clear"
                @click="handleClearEntry">C</button>
        <button class="equal"
                @click="calculate()">=</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      result: '',
      calculated: false                      // track if calculation has been done
    };
  },
  methods: {
    handleClick(value) {
      if (this.calculated) {                                   // If true, calculation has been done, 
        this.result = value;
        this.calculated = false;             
      } else {
        this.result += value;
      }
    },
    handleOperatorClick(operator) {                             // If the last character is an operator,replace it with the new operator
      if (/[+*/-]$/.test(this.result)) {
        this.result = this.result.slice(0, -1) + operator;
      } else {
        this.result += operator;
      }
      this.calculated = false;                                    // Reset 
    },
    
    handleClear() {
      this.result = '';
      this.calculated = false;               
    },
    handleClearEntry() {
      if (this.result && this.result.length > 0) {
        this.result = this.result.slice(0, -1);
        if (this.result.length === 0) {
          this.handleClear();
        }
      } else {
        this.handleClear();
      }
    },
    calculate() {
      try {
        this.result = eval(this.result);
      } catch (e) {
        console.error("Error in calculation", e);
      }
    }
  }
};
</script>

<style src="./style.css"></style>

