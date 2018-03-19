<template>
  <div id="home">
    <div id="calendar-form">
      <h1>Calendar</h1>

        <!-- CALENDAR COMPONENT -->
        <calendar :events="events" @selectedDay="selectedDay = $event" />
        <!-- EVENT FORM COMPONENT -->
        <event-form @eventCreated="addEvent" />
    </div>
    <div id="events">
      <!-- EVENT LIST COMPONENT -->
      <event-list :events="eventsSelected" />
    </div>
  </div>
</template>

<script>
import Calendar from '@/components/Calendar'
import EventList from '@/components/EventList'
import EventForm from '@/components/EventForm'

export default {
  name: 'Home',
  data () {
    return {
      // Initial events
      events: [
        { day: '20180328', description: 'CanariasJS meet-up!!' },
        { day: '20180329', description: 'Vacaciones' },
        { day: '20180423', description: 'Día del libro' }
      ],
      selectedDay: null
    }
  },
  computed: {
    eventsSelected () {
      return this.events.filter(e => e.day === this.selectedDay)
    }
  },
  methods: {
    addEvent (description) {
      this.events.push({
        day: this.selectedDay,
        description
      })
    }
  },
  components: {
    Calendar,
    EventList,
    EventForm
  }
}
</script>

<style lang="scss" scoped>
$page-padding: 10px;

#home {
  display: flex;
  padding: $page-padding;

  #calendar-form {
    flex: 1;
    height: calc(100vh - #{2 * $page-padding});
    margin: 20px;

    > *:first-of-type {
      margin-bottom: 30px;
    }
  }

  #calendar {
    margin-bottom: 30px;
  }

  #events {
    display: block;
    flex: 1;
    margin: 20px;
    height: 100%;
  }

  h1 {
    margin: 0 0 20px 0;
  }
}
</style>
