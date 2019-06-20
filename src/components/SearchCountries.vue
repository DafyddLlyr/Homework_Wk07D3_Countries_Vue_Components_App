<template lang="html">
  <input id="search" placeholder="Search..." type="text" v-model="search" @input="searchCountry">
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

#search {
  background-color: #81A4CD;
  font-weight: bold;
  border: none;
  margin: 3vw 0;
  padding: 0.4vw;
  font-size: 2rem;
  font-family: inherit;
  text-align: center;
  margin-left: 5vw;
}

</style>
