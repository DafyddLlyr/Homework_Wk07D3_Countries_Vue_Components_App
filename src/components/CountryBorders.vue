<template lang="html">
  <div>
    <p>Neighbours: <span v-for="borderingCountry in borders"> <a v-on:click="updateCountry(borderingCountry)">{{borderingCountry}}</a>&nbsp;</span></p>
  </div>

</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: 'country-borders',
  props: ['country', 'countries'],
  computed: {
    borders: function() {
      const threeLetterCountries = this.country.borders;
      const borderCountries = this.countries
      .filter(country => threeLetterCountries.includes(country.alpha3Code))
      .map(country => country.name)
      return borderCountries
    }
  },
  methods: {
    updateCountry: function(borderingCountry) {
      eventBus.$emit('country-borders', borderingCountry);
    }
  }
}
</script>

<style lang="css" scoped>
</style>
