<template>
  <div class="auto-loan-caculator">
    <p>Car Price</p>
    <input class="field--price" type="number" name="carPrice" v-model.number="carPrice" placeholder="">

    <p>Down Payment</p>
    <input class="field--down-payment" type="number" name="downPayment" v-model.number="downPayment" placeholder="">

    <p>Loan Duration (in months)</p>
    <input class="field--duration" type="number" name="loanDurationMonths" v-model.number="loanDurationMonths" placeholder="">

    <p>Interest Rate</p>    
    <input class="field--interest" type="number" name="interestRate" v-model.number="interestRate" placeholder="">

    <hr>

    <p>Estimated Monthly Payment</p>
    <div>{{ monthlyPayment }}</div>

    <p>Total Interest Paid (over duration of loan)</p>
    <div>{{ totalInterestPaid }}</div>
  </div>
</template>

<script>
  export default {
    name: 'auto-loan-caculator',
    data() {
      return {
        carPrice: '20000',
        downPayment: '10000',
        loanDurationMonths: '48',
        interestRate: '5',
        monthlyPayment: '',
        totalInterestPaid: '',
      }
    },
    props: {
      monthlyPayment: Number,
      totalInterestPaid: Number
    },
    computed: {
      monthlyPayment: function() {
        const principal = this.carPrice - this.downPayment;
        const monthlyInterestRate = this.interestRate / 100 / 12;
        const numberMonths = this.loanDurationMonths;

        // The meat and potatos calculation
        const estMonthlyAmount = principal * (monthlyInterestRate * (1 + monthlyInterestRate)**numberMonths) / ((1+monthlyInterestRate)**numberMonths-1) || 0;

        return Math.round(estMonthlyAmount);
      },
      totalInterestPaid: function() {
        const totalPrincipal = this.carPrice - this.downPayment;

        return this.loanDurationMonths * this.monthlyPayment - totalPrincipal;
      },
    }, 
  }
</script>

<style scoped>
  p {
    margin-bottom: 0;
  }

  input {
    margin-bottom: 1rem;
  }
</style>