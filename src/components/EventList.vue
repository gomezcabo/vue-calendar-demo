<template>
  <div id="event-list">
    <h1>Event List</h1>

    <!-- CONDITIONAL RENDERING -->
    <template v-if="events.length">
      <div class="event" v-for="(event, index) of events" :key="index">
        {{ event.description }}
      </div>
    </template>
    <div v-else>
      No events for this day
    </div>

  </div>
</template>

<script>
export default {
  props: {
    events: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style lang="scss" scoped>
#event-list {
  .event {
    padding: 15px 20px;
    border: 1px solid #ddd;
    margin: 8px 0;
  }
}

h1 {
  margin: -4px 0 34px 0;
}
</style>
