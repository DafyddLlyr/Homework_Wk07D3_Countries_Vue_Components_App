<template lang="html">
  <div v-if="country">
    <h1>{{ country.name }}</h1>
    <h2 v-if="nativeName !== country.name">{{ nativeName }}</h2>
    <p>Capital: {{ country.capital }}</p>
    <p>Population: {{ country.population }}</p>
    <p>Language: {{ languages }}</p>
    <country-borders :country="country" :countries="countries"></country-borders>
    <!-- <p v-if="borders">Neighbouring Countries: {{ borders }}</p> -->
    <img :src="country.flag" height="100">
  </div>
</template>

<script>
import CountryBorders from './CountryBorders.vue';

export default {
  name: 'country-details',
  props: ['country', 'countries'],
  computed: {
    languages: function(){
      const result = this.country.languages.map(language => language.name)
      return result.join(', ')
    },
    nativeName: function() {
      return this.country.nativeName;
    }
  },
  components: {
    'country-borders': CountryBorders
  }
}
</script>

<style lang="css" scoped>
</style>
