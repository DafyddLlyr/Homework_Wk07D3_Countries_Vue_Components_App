<template>
  <div id="app">
    <header>
      <h1>Vue Countries API App</h1>
    </header>
    <search-countries :countries="countries"></search-countries>
    <!-- <countries-select :countries="countries"></countries-select> -->
    <country-details :country="selectedCountry" :countries="countries"></country-details>
  </div>
</template>

<script>
import { eventBus } from './main.js'
import CountriesSelect from './components/CountriesSelect.vue';
import CountryDetails from './components/CountryDetails.vue';
import SearchCountries from './components/SearchCountries.vue';

export default {
  name: 'app',
  data(){
    return {
      countries: null,
      selectedCountry: null
    }
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(response => response.json())
    .then(countries => this.countries = countries)
    eventBus.$on(['country-selected', 'search'], (country) => {
      this.selectedCountry = country;
    })
    eventBus.$on('country-borders', borderingCountry => {
      this.selectedCountry = this.countries.filter(country => country.name === borderingCountry)[0]
    })
  },
  components: {
    'countries-select': CountriesSelect,
    'country-details': CountryDetails,
    'search-countries': SearchCountries
  }
}
</script>

<style>

body {
  display: flex;
  justify-content: center;
  background-color: #DBE4EE
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 50vw;
  background-color: #3E7CB1;
  border-radius: 20px;
}

header {
  background-color: #054A91;
  width: 100%;
}

h1 {
  color: #F17300;
}
</style>
