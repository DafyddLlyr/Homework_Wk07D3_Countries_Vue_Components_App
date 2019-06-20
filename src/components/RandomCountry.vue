<template lang="html">
  <i v-on:click="random" class="fas fa-random"></i>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: 'random-country',
  props: ['countries'],
  methods: {
    random: function() {
      const randomCountry = this.countries[Math.floor(Math.random()*250)];
      eventBus.$emit('random-country', randomCountry)
    }
  }
}
</script>

<style lang="css" scoped>

.fas {
  color: #F17300;
  font-size: 2.5rem;
  margin-left: 2vw;
  cursor: pointer;
}

</style>
