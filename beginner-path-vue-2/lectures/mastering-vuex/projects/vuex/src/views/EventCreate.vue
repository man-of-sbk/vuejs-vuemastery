<template>
  <div>
      <h1>Create an Event, {{ user.name }}</h1>
      <p>This event is created by {{ user.id }}</p>
      <p>There are {{ catLength }} categories</p>
  </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
  computed: {
    catLength() {
      return this.$store.getters.catLength
    },
    ...mapState(['categories', 'user'])
  }
}
</script>
