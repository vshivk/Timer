<template>
  <div>
    <div v-for="(timer, index) in timers" :key="index">
      <Timer :hours="timer.hours" :minutes="timer.minutes" :seconds="timer.seconds" />
    </div>
    <button @click="addTimer">Добавить таймер</button>
  </div>
</template>

<script>
import Timer from './TimeTracker.vue'

export default {
  name: 'TimerList',
  components: {
    Timer
  },
  data() {
    return {
      timers: [
        {
          hours: 0,
          minutes: 0,
          seconds: 0
        }
      ]
    }
  },
  methods: {
    addTimer() {
      this.timers.push({
        hours: 0,
        minutes: 0,
        seconds: 0
      })
    }
  }
}
</script>