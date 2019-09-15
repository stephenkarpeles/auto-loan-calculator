<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <section>
      <div class="container">
        <h1>Test</h1>
        <auto-loan-calculator/>
      </div>
    </section>    
  </div>
</template>

<script>
import AutoLoanCalculator from './components/AutoLoanCalculator.vue'

export default {
  name: 'app',
  components: {
    AutoLoanCalculator
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.container {
  width: 90%;
  margin: 0 auto;
}
</style>
