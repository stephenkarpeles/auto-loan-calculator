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
    <select name="loanDurationMonths" v-model.number="loanDurationMonths" >
        <option value="12">12 months</option>
        <option value="24">24 months</option>
        <option value="36">36 months</option>
        <option value="48">48 months</option>
        <option value="60" selected>60 months</option>
        <option value="72">72 months</option>
        <option value="84">84 months</option>
      </select>

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
    margin: 0;
  }

  input, 
  select {
    color: #333;
    border: 1px solid #333;
    width: 100%;
    font-size: 1.25rem;
    padding: 0 1rem;
    margin-bottom: 1.5rem;
    border-radius: 0;
    background: white;
    height: 50px;
    -webkit-appearance: none;
    appearance: none;
    
    &:focus {
      background-color: #fff;
      color: #3200ff;
      border-color: #3200ff;
      outline: 0;
    }
  
}
</style>