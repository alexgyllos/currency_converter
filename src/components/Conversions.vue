<template lang="html">
  <div class="contain">
  <!-- <form class="" v-on:submit.prevent>
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
  <button v-on:click="pinEuroToCurrency" type="button" name="button">Pin Conversion</button> -->

  <!-- <form v-on:submit.prevent>
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
  <button v-on:click="pinCurrencyToEuro" type="button" name="button">Pin Conversion</button> -->


  <div class="">
    <form class="" v-on:submit.prevent>
      <!-- <p>Convert Currencies</p> -->
      <div class="content">
        <div class="select">
          <label for="">Select Currency 1</label>
          <select v-model="base1" name="">
            <option disabled value=""></option>
            <option v-for="(conversionRate, currencyName) of conversionRates" :value="{name: currencyName, value: conversionRate}">{{currencyName}}</option>
          </select>
        </div>
        <br>
        <div class="select">
          <label for="">Enter Value</label>
          <input v-model="valueNonBase"type="number" name="" value="0">
        </div>
        <br>
        <div class="select">
          <label for="">Select Currency 2</label>
          <select v-model="base2" class="" name="">
            <option disabled value=""></option>
            <option v-for="(conversionRate, currencyName) of conversionRates" :value="{name: currencyName, value: conversionRate}">{{currencyName}}</option>
          </select>
        </div>

      </div>
      <br>
      <br>
      <button v-on:click="handleConversionWithoutBase" type="submit" name="button">Convert</button>
      <br>

      <p v-if="nonBaseResult"> Result:<span v-if="nonBaseResult"> {{this.base1name + " " + this.base1value + " = " + this.base2name + " " + this.nonBaseResult}} </span></p>
    </form>
    <hr>
  </div>
  <br>
  <button v-if="nonBaseResult" v-on:click="pinNonBase" type="button" name="button">Pin Conversion</button>
  <!-- <hr> -->
  <br>
  <p v-for="pin of pinned">{{pin}}</p>

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
      base1name: null,
      base1value: null,
      base2name: null,
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
      this.base2name = this.base2.name
      this.base1name = this.base1.name
      this.base1value = this.valueNonBase
      this.nonBaseResult = ((this.valueNonBase / this.base1.value) * (this.base2.value)).toFixed(2);
      this.valueNonBase = ""
      this.base1 = ""
      this.base2 = ""
      // <!-- (input / base1rate) * (base2rate) -->
    },
    pinNonBase: function() {
      this.pinned.push(this.base1name + " " + this.base1value + " = " + this.base2name + " " + this.nonBaseResult)
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
  .contain {
    text-align: left;
    /* border: 1px solid black; */
    display: flex;
    flex-direction: column;
    align-items: center;
    /* justify-content: center; */
    /* background-color:  */
    font-size: 1.2em;
  }

  .select {
    display: flex;
    flex-direction: column;
    margin: 5px;
    align-items: center;
    justify-content: center;
    /* padding: 5px; */
  }

  /* form {
    text-align: left;
  } */
  form {
    display: flex;
    flex-direction: column;
    flex-wrap: wrap;
    align-items: center;
    /* justify-content: center; */
    padding: 5%;
    /* border: 1px solid black; */
    width: 40vw;
    text-align: left;
    /* font-size: 1.2em; */
  }

  select {
    border: 1px solid white;
    /* text-align: center; */
    /* width: 100px; */
  }

  select:hover {
    cursor: pointer;
  }

  .eurosinput {
    border: 1px solid white;
  }

  input {
    border-bottom: 1px solid white;
    /* width: 60%; */
    width: 135px;
  }

  button {
    /* border: 1px solid white; */
  }

  button:hover {
    border-bottom: 1px solid white;
  }
</style>
