<template>
  <div class="container">
    <h1>Currency Converter</h1>
    <div class="">
      <hr>
      <conversions v-if="conversionRates" :conversionRates="conversionRates"></conversions>
    </div>
  </div>

</template>

<script>
import Conversions from './components/Conversions.vue'

export default {

  name: 'App',
  components: {
  },
  data () {
    return {
      conversionRates: []
    }
  },
  mounted() {
    fetch('https://api.exchangeratesapi.io/latest')
    .then(res => res.json())
    .then(data => this.conversionRates = data.rates)
    // .then(data => Object.assign(this.conversionRates, data.rates))
  },
  components: {
    'conversions': Conversions
  }
}
</script>

<style>
  html {
    background-image: url("https://images.unsplash.com/photo-1502920514313-52581002a659?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1647&q=80");
    background-attachment: fixed;
    background-repeat: no-repeat;
    background-size: cover;
    width: 100vw;
    height: 100vh;
    user-select: none;
  }

  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    border: 1px solid black;
    width: 50vw;
    margin: auto;
    margin-top: 7vh;
    background-color: black;
    opacity: 0.9;
    color: #e9c46a;
    margin-bottom: 7vh;
    border: 1px solid #e9c46a;
    font-size: 1.1em;
    font-family: 'Oswald', sans-serif;
  }
</style>
