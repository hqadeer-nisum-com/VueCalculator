<template>
  <div class="calculator">
    <div 
    class="display" v-if="this.isloading === false">{{current || '0'}} 
      </div>
      <div class="display" v-if="this.isloading === true">
        Loading...
      </div>
    
    <div @click="clear" class="btn cancel">C</div>
    
    <div @click="percent" class="btn">%</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiplication" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="minus" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('3')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
      isloading: false,
    }
  },
  watch: {
    // Creating function
    // for input component
    current: function() {

  if(this.isloading){
    setTimeout(()=>{ 
      this.isloading=false 
      }, 2000);
    }
 },

},
  methods: {
    clear(){
      this.current = '';
    },
  
    percent(){
      this.current = `${parseFloat(this.current) / 100}`
      this.isloading=true;
    },
    append(number){
      if(this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
    },
    dot(){
      if(this.current.indexOf('.')=== -1){
        this.append('.');
      }
    },
    setPrevious(){
      this.previous = this.current;
      this.operatorClicked = true;
    },
    divide(){
      this.operator = (a,b) => a / b;
      this.setPrevious();
    },
    multiplication(){
      this.operator = (a,b) => a * b;
      this.setPrevious();
    },
    minus(){
      this.operator = (a,b) => a - b;
      this.setPrevious();
    },
    add(){
      this.operator = (a,b) => a + b;
      this.setPrevious();
      
    },
    equal(){
      this.current = `${this.operator(parseFloat(this.previous),parseFloat(this.current)
     
      )}`;
      this.isloading=true;
      this.previous = null;
    
    }
    
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.calculator{
  width: 350px;
  margin: 0 auto;
  display: grid;
  font-size: 40px;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display{
  grid-column: 1/5;
  background-color: #2db34a;
  color: white;
}
.zero{
  grid-column: 1 / 3;
}

.btn{
  cursor: pointer;
  background-color: #eee;
  border: 1px solid lightgray;
}
.btn:hover{
  cursor: pointer;
  background-color:#333;
  color: white;
}
.operator{
  background-color: blanchedalmond;
  color: black;
}
.cancel{
  grid-column: 1/3;
}
</style>
