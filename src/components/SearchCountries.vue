<template lang="html">
  <input type="text" v-model="search" @input="searchCountry">
</template>

<script>
import { eventBus } from '../main.js'
export default {
  name: 'search-country',
  data() {
    return {
      search: null,
      selectedCountry: null
    }
  },
  methods: {
    searchCountry: function() {
      let result = this.countries.filter(country => country.name.toLowerCase().includes(this.search.toLowerCase()))
      result.sort((a, b) => a.name.length - b.name.length)
      this.selectedCountry = result[0]
      eventBus.$emit('search', this.selectedCountry)
    }
  },
  props: ['countries']
}
</script>

<style lang="css" scoped>
</style>
