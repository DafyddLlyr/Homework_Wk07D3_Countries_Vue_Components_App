<template lang="html">
  <select @change="handleChange" v-model="selectedCountry">
    <option value="">Select a country...</option>
    <option v-for="(country, index) in countries" :value="country" :key="index">{{ country.name }}</option>
  </select>
</div>

</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: 'countries-select',
  props: ['countries'],
  data() {
    return {
      selectedCountry: ""
    }
  },
  methods: {
    handleChange: function(){
      eventBus.$emit('country-selected', this.selectedCountry);
    }
  }
}
</script>

<style lang="css" scoped>
</style>
