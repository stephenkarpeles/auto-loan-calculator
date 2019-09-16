<template>
  <div class="auto-loan-caculator">
    <div class="form-field-row">
      <label for="carPrice" class="label label--price">Car Price</label><br>
      <input 
        class="form-field form-field--price" 
        type="number" 
        name="carPrice" 
        v-model.number="carPrice" 
        placeholder="">
    </div>

    <label for="downPayment" class="label label--price">Down Payment</label><br>
    <input 
      class="form-field form-field--down-payment" 
      type="number" 
      name="downPayment" 
      v-model.number="downPayment" 
      placeholder="">

    <p>Loan Duration (in months)</p>
    <input 
      class="form-field form-field--duration" 
      type="number" 
      name="loanDurationMonths"
      v-model.number="loanDurationMonths" 
      placeholder="">

    <p>Interest Rate</p>    
    <input 
      class="form-field form-field--interest" 
      type="number" 
      name="interestRate" 
      v-model.number="interestRate" 
      placeholder="">

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
        carPrice: '',
        downPayment: '',
        loanDurationMonths: '',
        interestRate: '',
        monthlyPayment: '',
        totalInterestPaid: '',
      }
    },
    props: {
      monthlyPayment: Number,
      totalInterestPaid: Number
    },
    computed: {
      totalPrincipal: function() {
        return this.carPrice - this.downPayment || 0;
      },
      monthlyPayment: function() {
        const monthlyInterestRate = this.interestRate / 100 / 12;
        const numberMonths = this.loanDurationMonths;

        // The meat and potatos calculation
        const estMonthlyAmount = this.totalPrincipal * (monthlyInterestRate * (1 + monthlyInterestRate)**numberMonths) / ((1+monthlyInterestRate)**numberMonths-1) || 0;

        return Math.round(estMonthlyAmount);
      },
      totalInterestPaid: function() {
        return this.loanDurationMonths * this.monthlyPayment - this.totalPrincipal || 0;
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
    padding: .5rem;
    align-self: center;
  }

  .form-field-row {
    display: flex;
  }

  .label {
    position: relative;
    width: 10rem;
    align-self: center;
  }

  .label:after {
    content: '$';
    left: 10.5rem;
    position: absolute;
  }
</style>