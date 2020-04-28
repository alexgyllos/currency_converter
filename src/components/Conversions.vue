<template lang="html">
  <div class="">
  <form class="" v-on:submit.prevent>
    <p>Convert Euros</p>
    <div>
      <label for="euros">Type in amount of Euros</label>
      <input class="eurosinput" type="number" name="euros" value="0" v-model="eurosTo">
    </div>
    <label for="">Select Currency</label>
    <select v-model="eurosToConversionRate" class="" name="c1">
      <option disabled value="">Choose Currency</option>
      <option v-for="(conversionRate, currencyName) of conversionRates" :value="{name: currencyName, value: conversionRate}">{{currencyName}}</option>
    </select>
    <button v-on:click="handleConversion" type="submit" name="button">Convert</button>
  </form>

  <p>Result: {{resultTo}}</p>
  <button v-on:click="pinEuroToCurrency" type="button" name="button">Pin Conversion</button>

  <form v-on:submit.prevent>
    <div class="">
      <p>Convert to Euros</p>
      <label for="">Select Currency</label>
      <select v-model="eurosFromConversionRate" class="" name="c2">
        <option disabled value="">Choose Currency</option>
        <option v-for="(conversionRate, currencyName) of conversionRates" :value="{name: currencyName, value: conversionRate}">{{currencyName}}</option>
      </select>
      <label for="">Type in Value</label>
      <input v-model="eurosFrom" type="number" name="" value="0">
      <button v-on:click="handleConversionToEuros" type="submit" name="button">Convert</button>
    </div>
  </form>

  <p>Result: {{resultFrom}}</p>
  <button v-on:click="pinCurrencyToEuro" type="button" name="button">Pin Conversion</button>


  <div class="">
    <form class="" v-on:submit.prevent>
      <div class="">
        <p>Convert Currencies</p>
        <label for="">Select Currency 1</label>
        <select v-model="base1" name="">
          <option disabled value="">Choose Currency</option>
          <option v-for="(conversionRate, currencyName) of conversionRates" :value="{name: currencyName, value: conversionRate}">{{currencyName}}</option>
        </select>
        <input v-model="valueNonBase"type="number" name="" value="0">
        <label for="">Select Currency 2</label>
        <select v-model="base2" class="" name="">
          <option disabled value="">Choose Currency</option>
          <option v-for="(conversionRate, currencyName) of conversionRates" :value="{name: currencyName, value: conversionRate}">{{currencyName}}</option>
        </select>
      </div>
      <button v-on:click="handleConversionWithoutBase" type="submit" name="button">Convert</button>
    </form>
  </div>

  <p>Result: {{nonBaseResult}}</p>
  <button v-on:click="pinNonBase" type="button" name="button">Pin Conversion</button>

  <p>Pinned: {{pinned}}</p>

  </div>


</template>

<script>
export default {
  name: 'conversions',
  data() {
    return {
      eurosTo: null,
      eurosToConversionRate: null,
      resultTo: null,
      eurosFrom: null,
      eurosFromConversionRate: null,
      resultFrom: null,
      base1: null,
      base2: null,
      valueNonBase: null,
      nonBaseResult: null,
      pinned: []
    }
  },
  props: ['conversionRates'],
  methods: {
    handleConversion: function() {
      this.resultTo = (this.eurosTo * this.eurosToConversionRate.value).toFixed(2);
    },
    handleConversionToEuros: function() {
      this.resultFrom = (this.eurosFrom / this.eurosFromConversionRate.value).toFixed(2);
    },
    handleConversionWithoutBase: function() {
      this.nonBaseResult = ((this.valueNonBase / this.base1.value) * (this.base2.value)).toFixed(2);
      // <!-- (input / base1rate) * (base2rate) -->
    },
    pinNonBase: function() {
      this.pinned.push(this.base1.name + " " + this.valueNonBase + " = " + this.base2.name + " " + this.nonBaseResult)
    },
    pinCurrencyToEuro: function() {
      this.pinned.push(this.eurosFromConversionRate.name + " " + this.eurosFrom + " = " + "EUR " + this.resultFrom)
    },
    pinEuroToCurrency: function() {
      this.pinned.push("EUR" + " " + this.eurosTo + " = " + this.eurosToConversionRate.name + " " + this.resultTo)
    }
  },
  watch: {
    todos: {
      handler() {
        console.log('Pinned changed!');
        localStorage.setItem('pinned', JSON.stringify(this.pinned));
      },
      deep: true,
    },
  },
  mounted() {
    console.log('App mounted!');
    if (localStorage.getItem('pinned')) this.pinned = JSON.parse(localStorage.getItem('pinned'));
  }
}
</script>

<style lang="css" scoped>
  select {
    border: 1px solid black;
  }

  .eurosinput {
    border: 1px solid black;
  }

  input {
    border: 1px solid black;
  }

  button {
    border: 1px solid black;
  }
</style>
