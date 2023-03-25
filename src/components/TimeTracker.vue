<template>
  <div :class="{'active-timer': active}">
    <div class="timer">{{ formatTime() }}</div>
    <button @click="startPause">{{ active ? 'Pause' : 'Start' }}</button>
    <button @click="reset">Reset</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hours: 0,
      minutes: 0,
      seconds: 0,
      intervalId: null,
      active: false
    }
  },
  methods: {
    startPause() {
      if (!this.active) {
        this.intervalId = setInterval(() => {
          if (++this.seconds === 60) {
            this.minutes++
            this.seconds = 0
          }
          if (this.minutes === 60) {
            this.hours++
            this.minutes = 0
          }
        }, 1000)
      } else {
        clearInterval(this.intervalId)
      }
      this.active = !this.active
    },
    reset() {
      this.hours = 0
      this.minutes = 0
      this.seconds = 0
      this.active = false
      clearInterval(this.intervalId)
    },
    formatTime() {
      const hh = this.hours.toString().padStart(2, '0')
      const mm = this.minutes.toString().padStart(2, '0')
      const ss = this.seconds.toString().padStart(2, '0')

      return `${hh}:${mm}:${ss}`
    }
  }
}
</script>

<style scoped>
.active-timer {
  background-color: gray;
}
</style>