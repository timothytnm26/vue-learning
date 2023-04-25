<script setup>
import CalculatorWrapper from '@/components/CalculatorWrapper.vue'
</script>
<template>
  <div class="calculator">
    <h1>CALCULATOR</h1>
    <CalculatorWrapper/>
  </div>
</template>

<style>

@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
  .calculator {
    color:white;
    font-weight: 500;
  font-size: 1.3rem;
  font-family: 'Courier New', Courier, monospace
  }
}
</style>
