<template>
  <div>
    <full-calendar
      :events="events"
      :plugins="calendarPlugins"
      :editable="true"
      contentHeight="auto"
      :theme="false"
      :selectable="true"
      :selectHelper="true"
      ref="fullCalendar"
      class="calendar"
      :defaultView="defaultView"
      @dateClick="onDateClick"
      @eventClick="onEventClick"
    >
    </full-calendar>
  </div>
</template>
<script>
import FullCalendar from '@fullcalendar/vue'
import dayGridPlugin from '@fullcalendar/daygrid'
import timeGridPlugin from '@fullcalendar/timegrid'
import interactionPlugin from '@fullcalendar/interaction'

const today = new Date()
const y = today.getFullYear()
const m = today.getMonth()

export default {
  name: 'calendar',
  components: {
    FullCalendar
  },
  data () {
    let yearAndMonth = `${y}-${m + 1}`
    return {
      calendarPlugins: [dayGridPlugin, timeGridPlugin, interactionPlugin],
      defaultView: 'dayGridMonth',
      events: [
        {
          title: 'Call with Dave',
          start: `${yearAndMonth}-18`,
          end: `${yearAndMonth}-18`,
          className: 'bg-red',
          allDay: true
        },

        {
          title: 'Lunch meeting',
          start: `${yearAndMonth}-21`,
          end: `${yearAndMonth}-22`,
          className: 'bg-orange',
          allDay: true
        },

        {
          title: 'All day conference',
          start: `${yearAndMonth}-29`,
          end: `${yearAndMonth}-29`,
          className: 'bg-green',
          allDay: true
        },

        {
          title: 'Meeting with Mary',
          start: `${yearAndMonth}-01`,
          end: `${yearAndMonth}-01`,
          className: 'bg-blue',
          allDay: true
        },

        {
          title: 'Winter Hackaton',
          start: `${yearAndMonth}-03`,
          end: `${yearAndMonth}-03`,
          className: 'bg-red',
          allDay: true
        },

        {
          title: 'Digital event',
          start: `${yearAndMonth}-07`,
          end: `${yearAndMonth}-09`,
          className: 'bg-orange',
          allDay: true
        },

        {
          title: 'Marketing event',
          start: `${yearAndMonth}-10`,
          end: `${yearAndMonth}-10`,
          className: 'bg-purple',
          allDay: true
        },

        {
          title: 'Dinner with Family',
          start: `${yearAndMonth}-19`,
          end: `${yearAndMonth}-19`,
          className: 'bg-red',
          allDay: true
        },

        {
          title: 'Black Friday',
          start: `${yearAndMonth}-23`,
          end: `${yearAndMonth}-23`,
          className: 'bg-blue',
          allDay: true
        },

        {
          title: 'Cyber Week',
          start: `${yearAndMonth}-02`,
          end: `${yearAndMonth}-02`,
          className: 'bg-yellow',
          allDay: true
        }
      ],
      showAddModal: false,
      showEditModal: false,
      model: {
        title: '',
        className: 'bg-default',
        description:
          'Nullam id dolor id nibh ultricies vehicula ut id elit. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.',
        start: '',
        end: ''
      },
      eventColors: [
        'bg-info',
        'bg-orange',
        'bg-red',
        'bg-green',
        'bg-default',
        'bg-blue',
        'bg-purple',
        'bg-yellow'
      ]
    }
  },
  methods: {
    calendarApi () {
      return this.$refs.fullCalendar.getApi()
    },
    changeView (viewType) {
      this.defaultView = viewType
      this.calendarApi().changeView(viewType)
    },
    next () {
      this.calendarApi().next()
    },
    prev () {
      this.calendarApi().prev()
    },
    onDateClick ({ date }) {
      this.showAddModal = true
      this.model.start = date
      this.model.end = date
    },
    onEventClick ({ el, event }) {
      console.log(el)
      this.model = {
        title: event.title,
        className: event.classNames ? event.classNames.join(' ') : '',
        start: event.start,
        end: event.end,
        description:
          'Nullam id dolor id nibh ultricies vehicula ut id elit. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.'
      }
      this.showEditModal = true
    },
    saveEvent () {
      if (this.model.title) {
        let event = {
          ...this.model,
          allDay: true
        }
        this.events.push(JSON.parse(JSON.stringify(event)))

        this.model = {
          title: '',
          eventColor: 'bg-danger',
          start: '',
          end: ''
        }
      }
      this.showAddModal = false
    },
    editEvent () {
      let index = this.events.findIndex(e => e.title === this.model.title)
      if (index !== -1) {
        this.events.splice(index, 1, this.model)
      }
      this.showEditModal = false
    },
    deleteEvent () {
      let index = this.events.findIndex(e => e.title === this.model.title)
      if (index !== -1) {
        this.events.splice(index, 1)
      }
      this.showEditModal = false
    }
  }
}
</script>
<style lang="scss">
@import '~@fullcalendar/core/main.css';
@import '~@fullcalendar/daygrid/main.css';
@import '~@fullcalendar/timegrid/main.css';
</style>
