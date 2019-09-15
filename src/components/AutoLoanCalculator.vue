<template>
  <div class="auto-loan-caculator">
    <p>Car Price</p>
    <input class="field--price" type="number" name="carPrice" v-model="carPrice" placeholder="$20,000">

    <p>Down Payment</p>
    <input class="field--down-payment" type="number" name="downPayment" v-model="downPayment" placeholder="$20,000">

    <p>Loan Duration (in months)</p>
    <input class="field--duration" type="number" name="loanDurationMonths" v-model="loanDurationMonths" placeholder="48">

    <p>Interest Rate</p>    
    <input class="field--interest" type="number" name="interestRate" v-model="interestRate" placeholder="8">

    <hr>

    <p>Monthly Payment</p>
    <input class="field--monthly-payment" type="text" id="monthlyPayment" v-model="monthlyPayment">

    <p>Total Interest Paid (over duration of loan)</p>
    <input class="field--interest-paid" type="text" id="totalInterestAmount" v-model="totalInterestAmount">
  </div>
</template>

<script>
  export default {
    name: 'auto-loan-caculator',
    data () {
      return {
        carPrice: '20000',
        downPayment: '10000',
        loanDurationMonths: '48',
        interestRate: '8',
      }
    },
    computed: {
      monthlyPayment: function() {
        return ( parseInt(this.carPrice) - parseInt(this.downPayment) ) * ((parseInt(this.interestRate)/12) * ((1 + (parseInt(this.interestRate)/12))**parseInt(this.loanDurationMonths))) / ( (1 + (parseInt(this.interestRate)/12))**parseInt(this.loanDurationMonths) - 1);
        // return parseInt(this.carPrice) + parseInt(this.downPayment);
      },
      totalInterestAmount: function() {
        return ;
      },
    }, 
  }
</script>

A= P*(r(1+r)^{n}) / ((1+r)^{n}-1)

A = the monthly payment.
P = the principal
r = the interest rate per month, which equals the annual interest rate divided by 12
n = the total number of months

<style scoped>
  p {
    margin-bottom: 0;
  }

  input {
    margin-bottom: 1rem;
  }
</style>