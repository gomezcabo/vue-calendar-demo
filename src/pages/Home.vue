<template>
  <div id="home">
    <div id="calendar-form">
      <div id="calendar">
        <h1>Calendar</h1>
        <calendar/>
      </div>
      <div id="form">
        <h1>New event</h1>
      </div>
    </div>
    <div id="events">
      <h1>Events</h1>
    </div>
  </div>
</template>

<script>
import Calendar from '@/components/Calendar'

export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components: {
    Calendar
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
$page-padding: 10px;

#home {
  display: flex;
  padding: $page-padding;

  #calendar-form {
    flex: 1;
    height: calc(100vh - #{2 * $page-padding});
  }

  #calendar {
    height: 50%;
  }

  #events {
    flex: 1;
  }

  h1 {
    margin: 0;
  }
}
</style>
