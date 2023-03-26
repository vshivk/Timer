<template>
  <div class="timer" :class="{ active: active }">
    <div class="timer-time">{{ formatTime() }}</div>
    <div class="timer-actions">
      <div class="timer-actions-item" @click="startPause">
        <span v-if="!active" class="timer-actions-start"></span>
        <span v-else class="timer-actions-pause">
          <span class="timer-actions-pause-stripe"></span>
          <span class="timer-actions-pause-stripe"></span>
        </span>
      </div>
      <div class="timer-actions-item">
        <span class="timer-actions-reset" @click="reset"></span>
      </div>
    </div>
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
          if (this.seconds === 59) {
            this.seconds = 0
            this.minutes++
          } else {
            this.seconds++
          }
          if (this.minutes === 60) {
            this.minutes = 0
            this.hours++
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
      const ss = this.seconds.toString().padStart(2, '0')
      const mm = this.minutes.toString().padStart(2, '0')

      if (this.minutes === 0) {
        return `${ss}`
      }
      if (this.hours === 0) {
        return `${mm}:${ss}`
      } else {
        const hh = this.hours.toString().padStart(2, '0')
        return `${hh}:${mm}:${ss}`
      }
    }
  },
  mounted() {
    this.formatTime()
  }
}
</script>

<style scoped>
.active .timer-time {
  color: #fff;
  border-color: #fff;
}

.active .timer-actions-start {
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent;
  border-left: 17px solid #fff;
  background: transparent;
}

.active .timer-actions-reset {
  background: #fff;
}

.timer {
  background: #696969;
  height: 120px;
  max-width: 225px;
  width: 100%;
  max-height: 120px;
}

.timer-time {
  display: flex;
  justify-content: center;
  padding: 20px 0;
  border-bottom: 1px solid #9E9E9E;
  color: #9E9E9E;
}

.timer-actions {
  display: flex;
  justify-content: center;
  padding: 20px 0;
  gap: 40px;
}

.timer-actions-start {
  display: inline-block;
  width: 0;
  height: 0;
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent;
  border-left: 17px solid #9E9E9E;
  background: transparent;
  transform: rotate(0deg);
  cursor: pointer;
}

.timer-actions-reset {
  width: 18px;
  height: 18px;
  background: #9E9E9E;
  border: none;
  cursor: pointer;
}

.timer-actions-item {
  display: flex;
  cursor: pointer;
  max-width: 20px;
  width: 100%;
}

.timer-actions-pause {
  display: flex;
  gap: 5px;
}

.timer-actions-pause-stripe {
  width: 3px;
  height: 20px;
  background-color: white;
}
</style>