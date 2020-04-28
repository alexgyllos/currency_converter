<template>
  <v-app>
    <conversions v-if="conversionRates" :conversionRates="conversionRates"></conversions>
  </v-app>
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
  },
  components: {
    'conversions': Conversions
  }
}
</script>
