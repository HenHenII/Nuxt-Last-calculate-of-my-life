<template>
  <div class="base">
    <div class="calculator">
      <div class="display">{{ currNum || 0 }} </div>
      <button class="btn calculator" @click="AppendNumber(7)">7</button>
      <button class="btn calculator" @click="AppendNumber(8)">8</button>
      <button class="btn calculator" @click="AppendNumber(9)">9</button>
      <button class="btn calculator" @click="GetOperator('+')">+</button>
      <button class="btn calculator" @click="AppendNumber(4)">4</button>
      <button class="btn calculator" @click="AppendNumber(5)">5</button>
      <button class="btn calculator" @click="AppendNumber(6)">6</button>
      <button class="btn calculator" @click="GetOperator('-')">-</button>
      <button class="btn calculator" @click="AppendNumber(1)">1</button>
      <button class="btn calculator" @click="AppendNumber(2)">2</button>
      <button class="btn calculator" @click="AppendNumber(3)">3</button>
      <button class="btn calculator" @click="GetOperator('*')">x</button>
      <button class="btn erase calculator" @click="DeleteNumber()">Del</button>
      <button class="btn calculator" @click="AppendNumber(0)">0</button>
      <button class="btn calculator" @click="SetDotOnNumber()">.</button>
      <button class="btn calculator" @click="GetOperator('/')">÷</button>
      <button class="clear calculator" @click="ClearNumber()">CLEAR</button>
      <button class="btn calculator" @click="Calculate()">=</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
        previousNum:'', //ก
        currNum:'', //เลขปัจจุบัน
        operator: '',
        oppress: false
    }
  },
  methods:{
      //Delete number
    DeleteNumber(){
      this.currNum = this.currNum.toString();
      this.currNum = this.currNum.slice(0, this.currNum.length-1);
    },
    //Clear number
    ClearNumber(){
      this.currNum = '';
    },
    //put a peroid sign into numbers
    SetDotOnNumber(){
        this.currNum = this.currNum.toString();
        if(!this.currNum.includes('.')){
            this.currNum = `${this.currNum}${'.'}`;
        }
    },
    AppendNumber(n){
        if(this.oppress){
            this.currNum = '';
            this.oppress = false;
        }
        this.currNum = `${this.currNum}${n}`;
    },
    GetOperator(op){
        this.operator = op;
        this.previousNum = this.currNum;
        this.oppress = true;
    },
    Calculate(){
        var tempCurrNum = this.currNum;
        switch(this.operator){
            case '+':{
                this.currNum = parseFloat(this.previousNum) + parseFloat(tempCurrNum);
            }break;
            case '-':{
                this.currNum = parseFloat(this.previousNum) - parseFloat(tempCurrNum);
            }break;
            case '*':{
                this.currNum = parseFloat(this.previousNum) * parseFloat(tempCurrNum);
            }break;
            case '/':{
                this.currNum = parseFloat(this.previousNum) / parseFloat(tempCurrNum);
            }break;
        }
        this.previousNum = '';
        this.operator = '';
    }
 } 
}
</script>
