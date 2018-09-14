<template>
  <div id="search" class="row justify-content-center">
    <div class="input-group mb-4 col-8">
      <b-form-input id="search-input" size="lg" type="text" placeholder="Search people by their colors"  @keyup.native="searchByColor"></b-form-input>
      <b-btn variant="dark" size="lg" slot="append">Search</b-btn>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import { EventBus } from '../events/event-bus.js'

export default {
  name: 'InputSearch',
  methods: {
    searchByColor: function (event) {
      const args = document.getElementById('search-input').value

      axios.get('http://127.0.0.1/people/search-by-color/color_' + args)
       .then(function (response) {
         EventBus.$emit('people-search', response.data)
         console.log(response)
       })
       .catch(function (error) {
         console.log(error)
       })
    }
  }
}
</script>

<style scoped></style>
