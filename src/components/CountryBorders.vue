<template lang="html">
  <div v-if="borders.length > 0">
    <p>Neighbours: <span v-for="(borderingCountry, index) in borders">
      <span v-if="index !=0">, </span>
      <a v-on:click="updateCountry(borderingCountry)">{{borderingCountry}}</a>
    </span></p>
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

p {
  font-size: 1.5rem;
}

a {
  text-decoration: underline;
  cursor: pointer;
}

a:hover {
  color: #DBE4EE;
}

</style>
