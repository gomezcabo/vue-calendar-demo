<template>
  <div>
    <h1>New event</h1>

    <!-- TWO WAY DATA BINDING -->
    <input
      type="text"
      placeholder="Event description"
      v-model="eventDescription"
      @keyup.enter="add"
    />

    <!-- EVENT BINDING -->
    <button @click="add">Add</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      eventDescription: ''
    }
  },
  methods: {
    add () {
      if (this.eventDescription.trim().length > 0) {
        this.$emit('eventCreated', this.eventDescription)
        this.eventDescription = ''
      }
    }
  }
}
</script>
