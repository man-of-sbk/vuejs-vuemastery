<template>
  <div>
      <h1>Create an Event, {{ user.name }}</h1>
      <p>This event is created by {{ user.id }}</p>
      <p>{{ getEventById(1) }}</p>
  </div>
</template>

<script>
import { mapState, mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters(['getEventById']),
    ...mapState(['categories', 'user'])
  }
}
</script>
