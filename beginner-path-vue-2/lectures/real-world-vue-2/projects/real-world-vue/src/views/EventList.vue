<template>
  <div>
    <h1>Events Listing</h1>
    <EventCard v-for="event in events" :key="event.id" :event="event"/>

    <router-link :to="{ name: 'event-show', params: { id: '1' } }">First Event</router-link>
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
import axios from 'axios' // <--- brings in the axios library

export default {
  data() {
    return {
      events: []
    }
  },
  components: {
    EventCard
  },
  created() {
    axios
      .get('http://localhost:3000/events')  // Does a get request
      .then(response => {
        this.events = response.data
      })
      .catch(error => {
        console.log('There was an error:', error.response) // Logs out the error
      })
  }
}
</script>
