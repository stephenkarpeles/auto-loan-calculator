<template>
  <div class="auto-loan-caculator">
    <div class="form-field-group">
      <label for="carPrice" class="label label--price">Car Price</label>
      <div class="form-field-wrap form-field-wrap--price">
        <input 
          class="form-field form-field--price" 
          type="number" 
          name="carPrice" 
          v-model.number="carPrice">
      </div>
    </div>

    <label for="downPayment" class="label label--price">Down Payment</label>
    <div class="form-field-wrap form-field-wrap--down-payment">
      <input 
        class="form-field form-field--down-payment" 
        type="number" 
        name="downPayment" 
        v-model.number="downPayment">
    </div>

    <label for="carPrice" class="label label--price">Loan Duration (in months)</label>
    <div class="form-field-wrap form-field-wrap--loan-duration">
      <select name="loanDurationMonths" v-model.number="loanDurationMonths" >
        <option value="12">12 months</option>
        <option value="24">24 months</option>
        <option value="36">36 months</option>
        <option value="48">48 months</option>
        <option value="60" selected>60 months</option>
        <option value="72">72 months</option>
        <option value="84">84 months</option>
      </select>
    </div>

    <label for="carPrice" class="label label--price">Interest Rate</label>
    <div class="form-field-wrap form-field-wrap--interest"> 
      <input 
        class="form-field form-field--interest" 
        type="number" 
        name="interestRate" 
        v-model.number="interestRate">
    </div>

    <div class="result-box">

      <h2>Estimated Monthly Payment:</h2>
      <div class="result__monthly-amount">$ {{ monthlyPayment }}</div>

      <h3>Total Interest Paid (over duration of loan)</h3>
      <div class="result__interest-paid">$ {{ totalInterestPaid }}</div>

    </div>
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
        const estMonthlyAmount = this.totalPrincipal * (monthlyInterestRate * (1 + monthlyInterestRate)**numberMonths) / ((1+monthlyInterestRate)**numberMonths-1);

        return Math.round(estMonthlyAmount) > 0 ? Math.round(estMonthlyAmount) : 0;
      },
      totalInterestPaid: function() {
        const totalInterest = this.loanDurationMonths * this.monthlyPayment - this.totalPrincipal;
        return totalInterest > 0 ? totalInterest : 0;
      },
    }, 
  }
</script>

<style scoped>
  p {
    margin: 0;
  }

  label {
    margin-bottom: .3rem;
    display: block;
    font-weight: 700;
  }

  input, 
  select {    
    padding: 0 1rem;
    margin-bottom: 1.5rem;
    border-radius: 0;
    background: white;
    height: 46px;
    width: 100%;
    border: 1px solid #999; 
    color: #333;   
    font-size: 1.25rem;
    -webkit-appearance: none;
    appearance: none;
  }

  input:focus,
  select:focus {
    background-color: #ecfcff;  
    border: 1px solid #333;  
    outline: 0;
  }

  select {
    cursor: pointer;
  }  

  input[type=number]::-webkit-inner-spin-button, 
  input[type=number]::-webkit-outer-spin-button { 
    -webkit-appearance: none; 
    margin: 0; 
  }

  .form-field--price,
  .form-field--down-payment {
    padding-left: 1.6rem;
  }

  .form-field-wrap {
    position: relative;
  }

  .form-field-wrap:after {
    position: absolute;
    display: inline-block;
  }

  .form-field-wrap--price:after,
  .form-field-wrap--down-payment:after {
    content: '$';
    left: .75rem;
    top: .65rem;
    font-size: 1.25rem;
  }

  .form-field-wrap--interest:after {
    content: '%';
    right: .75rem;
    top: .65rem;
    font-size: 1.25rem;
  }

  .form-field-wrap--loan-duration:after {
    content: '\232a';
    transform: rotate(90deg);
    right: 1.25rem;
    top: 1rem;
    font-size: 1.25rem;
    pointer-events: none;
  }

  .result__monthly-amount {
    margin-bottom: 1rem;
  }

  .result-box {
    background: #ecfcff;
    padding: 1rem 1rem 1.25rem 1rem;
  }

  .result-box h2,
  .result-box h3 {
    margin-bottom: .5rem;
  }

  .result__monthly-amount {
    font-size: 2.05rem;
    color: #3e64ff;
    font-weight: 700;
    margin-bottom: 1.75rem;
  }

  .result__interest-paid {
    font-weight: 700;
    font-size: 1.5rem;
    color: #333;
  }
</style>