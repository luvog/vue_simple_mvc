<template>
  <div id="people-box" class="row justify-content-center">
    <div class="mb-4 col-8">
      <b-jumbotron header="Different People!">
        <PersonCard v-for="person in this.people" :key="person.person_id" :person="person" v-if="people.length > 0"/>
        <h3 v-show="people.length === 0">There is no people!</h3>
      </b-jumbotron>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import PersonCard from './PersonCard.vue'
import { EventBus } from '../events/event-bus.js'

export default {
  name: 'PeopleBox',
  components: {
    PersonCard
  },
  data: function () {
    return {
      people: []
    }
  },
  methods: {
    getAll: function (event) {
      axios.get('http://127.0.0.1/people/get-all')
       .then(response => {
         console.log(response)
         this.people = response.data
       })
       .catch(error => {
         console.log(error)
       })
    }
  },
  mounted: function () {
    this.getAll()

    EventBus.$on('people-search', people => {
      this.people = this.people.slice(this.people.length)
      this.people = this.people.concat(people)
    })
  }
}
</script>

<style scoped>
h1 {
  font-size: 3em;    
}
.jumbotron {
  padding: 2.5rem 2rem 4rem 2rem;
}
</style>
