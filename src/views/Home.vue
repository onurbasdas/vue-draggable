<template>
  <div>
    <b-card class="headerCard"> </b-card>
    <b-row>
      <b-col md="4">
        <b-card class="sideCard">
          <draggable
            tag="ul"
            group="all-users"
            class="draggable-list"
            ghost-class="moving-card"
            filter=".action-button"
            :list="test"
            :animation="200"
          >
            <li v-for="tes in test" :key="tes.name">
              <p>{{ tes.title }}</p>
            </li>
          </draggable>
        </b-card>
      </b-col>
      <b-col>
        <draggable
          tag="ul"
          group="all-users"
          class="draggable-list"
          ghost-class="moving-card"
          filter=".action-button"
          :list="events"
          :animation="200"
        >
          <full-calendar
            :config="config"
            :events="events"
            :selectable="true"
            @select="handleSelect"
            @clickDate="handleDateClick"
            class="calendar"
          >
          </full-calendar>
        </draggable>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import moment from 'moment'
import Draggable from 'vuedraggable'

export default {
  components: {
    Draggable
  },
  data () {
    return {
      events: [
        {
          title: 'test',
          allDay: true,
          start: moment(),
          end: moment().add(1, 'd')
        },
        {
          title: 'another test',
          start: moment().add(2, 'd'),
          end: moment()
            .add(2, 'd')
            .add(2, 'h')
        }
      ],
      config: {
        defaultView: 'month',
        selectable: true
      },
      test: [
        {
          title: 'test',
          allDay: true,
          start: moment(),
          end: moment().add(10, 'd')
        },
        {
          title: 'another test',
          start: moment().add(4, 'd'),
          end: moment()
            .add(2, 'd')
            .add(2, 'h')
        }
      ]
    }
  },
  methods: {
    handleDateClick (e) {
      console.log(e)
    },
    handleSelect (e) {
      console.log(e)
    }
  }
}
</script>

<style scoped>
.sideCard {
  position: fixed;
  display: absolute;
  top: 50px;
  left: 0px;
  min-height: 80vh;

  max-width: 300px;
}
.draggable-list {
  height: 100px;
}
.moving-card {
  opacity: 0.5;
  background: #f7fafc;
  border: 1px solid #4299e1;
}
.calendar {
  position: fixed;
  display: absolute;
  top: 100px;
  left: 200px;
}
.headerCard {
  position: fixed;
  display: absolute;
  top: 0px;
  left: 200px;
  width: 100%;
  height: 80px;
}
</style>
