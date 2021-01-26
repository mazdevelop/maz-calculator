<template>
	<div class="bg-gray-100	 h-screen w-full grid place-items-center">
		<div class="grid shadow-xl rounded-md border border-gray-400 w-96 h-96 px-4 ">
			<input type="text" class="appearance-none h-16 w-full bg-gray-100 border-b border-red-300 mb-2 outline-none text-right text-3xl  " v-model="result" disabled>
			<div class="grid grid-cols-4  h-16 gap-3">
				<button class="w-25 h-10 text-xl" @click="clear">C</button>
				<button class="w-25 h-10 text-xl" @click="invert">+/-</button>
				<button class="w-25 h-10 text-xl" @click="percent">%</button>
				<button class="w-25 h-10 text-xl" @click="setOperator('/')">/</button>
			</div>
			<div class="grid grid-cols-4 h-16 gap-3">
				<button class="w-25 h-10 text-xl" @click="addNumber(7)">7</button>
				<button class="w-25 h-10 text-xl" @click="addNumber(8)">8</button>
				<button class="w-25 h-10 text-xl" @click="addNumber(9)">9</button>
				<button class="w-25 h-10 text-xl" @click="setOperator('*')">*</button>
			</div>
			<div class="grid grid-cols-4  h-16 gap-3">
				<button class="w-25 h-10 text-xl" @click="addNumber(4)">4</button>
				<button class="w-25 h-10 text-xl" @click="addNumber(5)">5</button>
				<button class="w-25 h-10 text-xl" @click="addNumber(6)">6</button>
				<button class="w-25 h-10 text-xl" @click="setOperator('-')">-</button>
			</div>
			<div class="grid grid-cols-4  h-16 gap-3">
				<button class="w-25 h-10 text-xl" @click="addNumber(1)">1</button>
				<button class="w-25 h-10 text-xl" @click="addNumber(2)">2</button>
				<button class="w-25 h-10 text-xl" @click="addNumber(3)">3</button>
				<button class="w-25 h-10 text-xl" @click="setOperator('+')">+</button>
			</div>
			<div class="grid grid-cols-4 h-16 gap-3">
				<button class="w-25 h-10 text-xl col-span-2" @click="addNumber(0)">0</button>
				<button class="w-25 h-10 text-xl" @click="addPoint">.</button>
				<button class="w-25 h-10 text-xl" @click="equal">=</button>
			</div>
		</div>
	</div>
</template>
<script>
	export default {
    data(){
      return{
        result:0,
        tmp_value:0,
        reset:false,
        operator:undefined,
      }
    },
    methods:{
      clear(){
         this.result =0;
         this.tmp_value = 0;     
         this.operator =  undefined;
      },
      invert(){
        this.result *=-1;
      },
      percent(){
        this.result /= 100;
      },
      addNumber(num){
        if(this.result == 0 || this.reset === true){
            this.result ='';
            this.reset = false;
        }
        this.result += num.toString();
      },
      addPoint(){
        if(!this.result.includes('.'))
          this.result += '.';
      },
      setOperator(operator){
        if(this.tmp_value != 0)
          this.calculate();
        this.tmp_value = this.result;
        this.operator =operator;
        this.reset = true
      },
      calculate(){
        let value = 0;
        let fristNum = parseFloat(this.tmp_value);
        let secondNum = parseFloat(this.result);
        let map = {
          '+' : fristNum + secondNum,
          '-' : fristNum - secondNum,
          '*' : fristNum * secondNum,
          '/' : fristNum / secondNum,
        };
        value = map[this.operator];
        this.result = value.toString();
      },
      equal(){
        this.calculate();
        this.tmp_value = 0;
        this.operator = undefined;
      }
    },
     computed:{
      
    },
  };
</script>
<style lang="scss" scoped>
</style>