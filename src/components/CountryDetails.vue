<template lang="html">
  <div v-if="country" id="country-details">
    <h2>{{ country.name }}</h2>

    <h3 v-if="nativeName !== country.name">{{ nativeName }}</h3>

      <p>Capital: {{ country.capital }}</p>
      <p>Population: {{ country.population.toLocaleString() }}</p>
      <p>Language: {{ languages }}</p>
      <img :src="country.flag" height="150px">
    <country-borders :country="country" :countries="countries"></country-borders>

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

#country-details {
  width: 90%;
  margin-bottom: 2vw;
}

h2 {
  font-size: 3rem;
  margin: 0;
  margin-top: -2vw;
}

h3 {
  font-size: 1.5rem;
  font-style: italic;
  margin: 0;
}

p {
  font-size: 1.5rem;  
}

</style>
