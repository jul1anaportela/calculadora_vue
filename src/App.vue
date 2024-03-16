<script setup>
import { reactive } from 'vue';

const operationApp = reactive({
  number1: null,
  number2: null,
  operation: 'select',
  result: null
});

let previousNumber1 = null;
let previousNumber2 = null;

const calculateResult = () => {
  const a = parseFloat(operationApp.number1);
  const b = parseFloat(operationApp.number2);

  // Verificar se os números são válidos
  if (isNaN(a) || isNaN(b)) {
    operationApp.result = null;
    return;
  }

  // Armazenar números anteriores
  previousNumber1 = operationApp.number1;
  previousNumber2 = operationApp.number2;

  switch (operationApp.operation) {
    case 'sum':
      operationApp.result = a + b;
      break;
    case 'subtract':
      operationApp.result = a - b;
      break;
    case 'division':
      // Verificar divisão por zero
      if (b === 0) {
        operationApp.result = null;
      } else {
        operationApp.result = a / b;
      }
      break;
    case 'multiply':
      operationApp.result = a * b;
      break;
    default:
      operationApp.result = null;
  }

  // Limpar inputs apenas se a operação for válida
  operationApp.number1 = null;
  operationApp.number2 = null;
};

// Definir função para obter o símbolo da operação
const getOperationSymbol = (operation) => {
  switch (operation) {
    case 'sum':
      return '+';
    case 'subtract':
      return '-';
    case 'division':
      return ':';
    case 'multiply':
      return 'x';
    default:
      return '';
  }
};
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Calculator</h1>
    </header>
    <form @submit.prevent="calculateResult">
      <div class="row">
        <div class="col-md-2">
          <input type="number" class="form-control" v-model="operationApp.number1">
        </div>
        <div class="col-md-2">
          <select class="form-control" v-model="operationApp.operation">
            <option value="select">select</option>
            <option value="sum">+</option>
            <option value="subtract">-</option>
            <option value="division">:</option>
            <option value="multiply">x</option>
          </select>
        </div>
        <div class="col-md-2">
          <input type="number" class="form-control" v-model="operationApp.number2">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">result</button>
        </div>
      </div>
      <div class="row mt-5">
        <h4>Result:</h4>
        <span>{{ previousNumber1 }} {{ getOperationSymbol(operationApp.operation) }} {{ previousNumber2 }} = {{ operationApp.result !== null ? operationApp.result : '' }}</span>
      </div>
    </form>
  </div>
</template>

<style scoped></style>
