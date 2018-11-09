<template>
  <div class="calendar">

    <!-- PREV/NEXT actions & HEADER -->
    <div class="actions">
      <a @click="prevMonth"> ⇠ </a>
      <div class="month">{{ monthName }} {{ year }}</div>
      <a @click="nextMonth"> ⇢ </a>
    </div>

    <!-- DAY NAMES HEADER -->
    <div v-for="day of weekDays" :key="'header' + day" class="day header">
      {{ day }}
    </div>

    <!-- EXTRA DAYS BEFORE -->
    <template v-if="extraDaysBefore > 0">
      <div v-for="day of extraDaysBefore" :key="'pre' + day" class="day empty">
        <!-- empty -->
      </div>
    </template>

    <!-- MONTH DAYS -->
    <div
      v-for="day of daysInMonth"
      :key="day"
      class="day"
      :class="{ 'selected': isSelectedDay(day), 'has-tasks': dayHasTasks(day) }"
      @click="selectDay(day)"
    >
      {{ day }}
    </div>

  </div>
</template>

<script>
import moment from 'moment'
import weekDays from '@/constants/weekDays'
import monthNames from '@/constants/monthNames'

const today = moment()

export default {
  props: {
    tasks: {
      type: Array
    }
  },
  data () {
    return {
      // CURRENT MONTH, YEAR AND SELECTED DAY
      month: today.month(),
      year: today.year(),
      selectedDay: null
    }
  },
  computed: {
    // CONSTANTS
    today: () => today,
    weekDays: () => weekDays,
    monthNames: () => monthNames,

    // CURRENT MONTH
    currentMonth () {
      return moment().year(this.year).month(this.month)
    },
    // NUMBER OF DAYS IN MONTH
    daysInMonth () {
      return this.currentMonth.daysInMonth()
    },
    // EXTRA DAYS
    extraDaysBefore () {
      return this.currentMonth.startOf('month').day() - 1
    },
    monthName () {
      return this.monthNames[this.month]
    }
  },
  methods: {
    prevMonth () {
      if (this.month !== 0) {
        this.month--
      } else {
        this.month = 11
        this.year--
      }
    },
    nextMonth () {
      if (this.month !== 11) {
        this.month++
      } else {
        this.month = 0
        this.year++
      }
    },
    isSelectedDay (day) {
      const currentDay = moment().year(this.year).month(this.month).date(day).format('YYYYMMDD')
      return this.selectedDay && currentDay === this.selectedDay.format('YYYYMMDD')
    },
    dayHasTasks (day) {
      const currentDay = moment().year(this.year).month(this.month).date(day).format('YYYYMMDD')
      return !!this.tasks.find(e => e.day === currentDay)
    },
    selectDay (day) {
      this.selectedDay = moment().year(this.year).month(this.month).date(day)
      this.$emit('selectedDay', this.selectedDay.format('YYYYMMDD'))
    }
  }
}
</script>

<style lang="scss" scoped>
.data {
  width: 100%;
  display: block;
}
.calendar {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  border: 1px solid #eee;
  box-shadow: 1px 1px 10px 0px rgba(0,0,0,0.15);
  padding-bottom: 10px;

  .actions {
    display: flex;
    width: 100%;
    justify-content: space-between;
    align-items: center;
    padding: 2px;
    margin-bottom: 10px;
    font-weight: bold;

    .month {
      color: #de3800;
      font-size: 22px;
    }

    a {
      margin: 10px 20px;
      padding: 10px 20px;
      border-radius: 4px;
      cursor: pointer;

      &:hover {
        background-color: #eeeeee;
      }
    }
  }

  .day {
    width: calc(100% * (1/7) - 24px);
    padding: 10px 6px;
    border-radius: 3px;
    margin: 6px 6px;
    position: relative;
    display: inline-block;

    text-align: center;
    color: darkslategray;

    &.empty {
      background: white;
    }

    &.header {
      background: transparent;
      font-weight: bold;
    }

    &.has-tasks {
      font-weight: bold;
      color: darken(#de3800, 0%);
      background-color: rgba(#de3800, 0.1);
      text-decoration: underline;
    }

    &.selected {
      background-color: rgba(#3063CF, 0.9);
      cursor: default;
      color: white;
    }

    &:not(.empty):not(.header):not(.selected):hover {
      cursor: pointer;
      background-color: #eeeeee;
    }
  }
}
</style>
