<template>
  <div>
    <h1>Events Listing</h1>
    <EventCard/>

    <router-link :to="{ name: 'event-show', params: { id: '1' } }">First Event</router-link>
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'; // import the EventsCard component

export default {
  components: {
    EventCard, // register the EventsCard as a child component
  }
}
</script>
