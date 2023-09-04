<template>
 <div class="container">
  <div class="display">{{ display || 0 }}</div>

  <div @click="clear" class="operands">C</div>
  <div @click="percent" class="operands">&#x25;</div>
  <div @click="backspace" class="operands">&#8592;</div>
  <div @click="divide" class="operands">&divide;</div>

  <div @click="getDigit('7')" class="digits">7</div>
  <div @click="getDigit('8')" class="digits">8</div>
  <div @click="getDigit('9')" class="digits">9</div>

  <div @click="multiply" class="operands">&#215;</div>

  <div @click="getDigit('4')" class="digits">4</div>
  <div @click="getDigit('5')" class="digits">5</div>
  <div @click="getDigit('6')" class="digits">6</div>

  <div @click="minus" class="operands">&#8722;</div>

  <div @click="getDigit('1')" class="digits">1</div>
  <div @click="getDigit('2')" class="digits">2</div>
  <div @click="getDigit('3')" class="digits">3</div>

  <div @click="plus" class="operands">&#43;</div>

  <div @click="getDigit('00')" class="digits">00</div>
  <div @click="getDigit('0')" class="digits">0</div>
  <div @click="dot" class="digits">.</div>
  <div @click="equal" class="operands">&#61;</div>
 </div>
</template>

<script>

export default {
  name: 'CalculatorPage',

  components: {
    
  },

  data() {
    return {
      display: "",
      equation: "",
      errorCaught: false
    }
    
  },
  methods: {
    clear() {
      // clear result screen
      this.display = "";
      this.equation = "";
      this.operator = null;
      this.previousClick = null;
      
    },
    backspace() {
      this.display = this.display.replace(this.display[this.display.length - 1], "")
    },  
    getDigit(digit) {
      if(this.errorCaught){
        this.display = "";
        this.equation = "";
        this.errorCaught = false;
      }
      this.display += digit;
      this.equation += digit;
    },
    percent() {
      if(this.errorCaught){
        this.display = "";
        this.equation = "";
        this.errorCaught = false;
      }
      this.display += '%'
      this.equation += '*0.01'
    },
    divide() {
      if(this.errorCaught){
        this.display = "";
        this.equation = "";
        this.errorCaught = false;
      }
      this.display += '÷'
      this.equation += '/'
    },
    multiply() {
      if(this.errorCaught){
        this.display = "";
        this.equation = "";
        this.errorCaught = false;
      }
      this.display += '×'
      this.equation += '*'
    },
    plus() {
      if(this.errorCaught){
        this.display = "";
        this.equation = "";
        this.errorCaught = false;
      }
      this.display += '+'
      this.equation += '+'
    },
    minus() {
      if(this.errorCaught){
        this.display = "";
        this.equation = "";
        this.errorCaught = false;
      }
      this.display += '-'
      this.equation += '-'
    },
    dot() {
      if(this.errorCaught){
        this.display = "";
        this.equation = "";
        this.errorCaught = false;
      }
      this.display += '.'
      this.equation += '.'
    },
    equal() {
      try {
        if(this.equation != null && this.display != null){
          this.display = eval(this.equation)
          this.equation = this.display
        }
      } catch (error) {
        this.display = "Expression Error"
        this.equation= "Expression Error";
        this.errorCaught = true;
      }
    }
  }
}
</script>

