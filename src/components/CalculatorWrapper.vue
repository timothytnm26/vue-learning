<template>
    <div class="calculator-wrapper">
        <div class="cal-container">
            <div class="result">
                <p>{{ this.displayVal }}</p>
            </div>
            <div class="cal-buttons">
                <button @click="this.clearDisplay()">C</button>
                <button >ANS</button>
                <button @click="this.del()">DEL</button>
                <button @click="this.applyOperator('/')">/</button>
                <button @click="this.appendToDisplay('7')">7</button>
                <button @click="this.appendToDisplay('8')">8</button>
                <button @click="this.appendToDisplay('9')">9</button>
                <button @click="this.applyOperator('*')">*</button>
                <button @click="this.appendToDisplay('4')">4</button>
                <button @click="this.appendToDisplay('5')">5</button>
                <button @click="this.appendToDisplay('6')">6</button>
                <button @click="this.applyOperator('-')">-</button>
                <button @click="this.appendToDisplay('1')">1</button>
                <button @click="this.appendToDisplay('2')">2</button>
                <button @click="this.appendToDisplay('3')">3</button>
                <button @click="this.applyOperator('+')">+</button>
                <button>^^</button>
                <button @click="this.appendToDisplay('0')">0</button>
                <button @click="this.appendToDisplay('.')">.</button>
                <button @click="this.equals">=</button>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'CalculatorWrapper',
    data() {
        return {
            displayVal: "0",
            operator: null,
            firstNumber: 0,
            secondNumber: 0,
            clearDisplayNext: false,
        }
    },
    methods: {
        appendToDisplay(val) {
            if(this.displayVal=="0"){
                this.displayVal = val;
            } else this.displayVal += val;
        },
        del(){
            if(this.displayVal.length>1){
                this.displayVal = this.displayVal.slice(0, -1);
            } else this.displayVal = 0;
        },
        clearDisplay() {
            this.displayVal = 0;
            this.clearDisplayNext = false;
        },
        clearCalculator() {
            this.clearDisplay();
            this.clearCalculation();
        },
        clearCalculation() {
            this.operator = null;
            this.firstNumber = 0;
            this.secondNumber = 0;
        },
        applyOperator(operator) {
            console.log('o',operator)
            const operatorExist = this.operator !== null;
            const currentNumber = parseFloat(this.displayValue);
            if (!operatorExist) {
                this.displayVal += operator;
                this.firstNumber = currentNumber;
                this.operator = operator;
            }
        },
        equals() {
            this.secondNumber = parseFloat(this.displayValue);
            console.log(this.firstNumber, this.operator, this.secondNumber)
            this.calculate();
        },
        calculate() {
            const firstNumber = this.firstNumber;
            const secondNumber = this.secondNumber;
            const operator = this.operator;
            let result = 0;
            switch (operator) {
                case '+':
                    result = firstNumber + secondNumber;
                    break;
                case '-':
                    result = firstNumber - secondNumber;
                    break;
                case '*':
                    result = firstNumber * secondNumber;
                    break;
                case '/':
                    result = firstNumber / secondNumber;
                    break;
            }
            this.displayVal = result;
        },
    }, computed: {
        calculations() {
            return this.$store.state.calculations;
        },
        lastAnswer() {
            return this.$store.getters.lastAnswer;
        },
    },
}
</script>
<style>
.calculator-wrapper{
    max-width: 400px;
}
.result{
    border: 1px solid white;
    font-family: 'Courier New', Courier, monospace;
    font-size: 40px;
    text-align: end;
    padding: 0 10px;
    height: 70px;
}
.cal-buttons{
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 10px;
    padding-top: 10px;
}
.cal-buttons button {
    border: 1px solid white;
    background: transparent;
    color: white;
    font-family: 'Courier New', Courier, monospace;
    font-size: 30px;
    padding: 10px;
    cursor: pointer;
    outline: none;
}
.cal-buttons button:hover{
    background: rgb(219, 219, 219);
    color: black;
}
</style>