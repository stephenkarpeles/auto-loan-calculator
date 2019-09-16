<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <section class="calc-wrapper">
      <div class="calc-container">
        <h1>Auto Loan Calculator</h1>
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
}

html {
  background: url(./assets/car-bg.jpg) no-repeat center center fixed; 
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

html,
body {
  margin: 0;
  padding: 0;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  margin-top: 0;
}

.calc-wrapper {
  margin-top: 5rem;
}

.calc-container {
  width: 22rem;
  max-height: 90%;
  margin: 0 auto;
  background: white;
  color: #333;
  text-align: center;
  padding: 1.75rem 3rem;
  border-radius: .5rem;
}
</style>
