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
@import url('https://fonts.googleapis.com/css?family=Nunito+Sans:400,700&display=swap');

#app {
  font-family: 'Nunito Sans', Helvetica, Arial, sans-serif;
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

h1 {
  font-size: 1.75rem;
  margin-bottom: 1.5rem;
  line-height: 1.1;
}

h2 {
  line-height: 1.15;
}

h3 {
  line-height: 1.15;
}

.calc-wrapper {
  margin: 5rem 0;
}

.calc-container {
  width: 23em;
  max-width: 90%;
  margin: 0 auto;
  background: white;
  color: #333;
  text-align: center;
  padding: 2rem 2.75rem 2.25rem 2.75rem;
  border-radius: .5rem;
  box-shadow: 0 1px 10px rgba(0, 0, 0, 1);
}

@media only screen and (max-width: 599px) {
  .calc-wrapper {
    margin: 3rem 0;
  }

  .calc-container {
    padding: 1.25rem 1.5rem;
  }
}
</style>
