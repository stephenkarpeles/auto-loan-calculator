<template>
  <div class="auto-loan-caculator">
    <input type="number" name="number1" v-model="number1">
    <p>+</p>
    <input type="number" name="number2" v-model="number2">
    <p>=</p>
    <hr>
    <input type="text" id="result" v-model="result">
  </div>
</template>

<script>
  export default {
    name: 'auto-loan-caculator',
    data () {
      return {
        number1: '',
        number2: '',
      }
    },
    computed: {
      result: function(){
          return parseInt(this.number1) + parseInt(this.number2);
      }
    }, 
  }
</script>

<style scoped>
</style>