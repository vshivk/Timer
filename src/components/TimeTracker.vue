<template>
  <div class="timer" :class="{ active: isTimerActive }">
    <div class="timer-time">{{ formattedTime }}</div>
    <div class="timer-controls">
      <div class="timer-controls-toggle" @click="toggleTimer">
        <span v-if="!isTimerActive" class="timer-controls-toggle-start"></span>
        <span v-else class="timer-controls-toggle-pause">
          <span class="timer-controls-toggle-pause-stripe"></span>
          <span class="timer-controls-toggle-pause-stripe"></span>
        </span>
      </div>
      <div class="timer-controls-reset">
        <span class="timer-controls-reset-icon" @click="resetTimer"></span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    timer: {
      type: Object,
      required: true
    },
  },
  data() {
    return {
      intervalId: null,
      isTimerActive: false
    };
  },
  methods: {
    toggleTimer() {
      if (!this.isTimerActive) {
        this.intervalId = setInterval(() => {
          this.incrementTimer();
        }, 1000);
      } else {
        this.stopTimer();
      }
      this.isTimerActive = !this.isTimerActive;
    },
    stopTimer() {
      clearInterval(this.intervalId);
    },
    incrementTimer() {
      const newSeconds = this.timer.seconds + 1;
      const newMinutes = this.timer.minutes + (newSeconds === 60 ? 1 : 0);
      const newHours = this.timer.hours + (newMinutes === 60 ? 1 : 0);
      const updatedTimer = {
        ...this.timer,
        hours: newHours >= 24 ? 0 : newHours,
        minutes: newMinutes % 60,
        seconds: newSeconds % 60
      };
      this.$emit('update-timer', updatedTimer);
    },
    resetTimer() {
      const updatedTimer = {
        ...this.timer,
        hours: 0,
        minutes: 0,
        seconds: 0
      };
      this.$emit('update-timer', updatedTimer);
      this.stopTimer();
      this.isTimerActive = false;
    }
  },
  computed: {
    formattedTime() {
      const ss = this.timer.seconds.toString().padStart(2, '0');
      const mm = this.timer.minutes.toString().padStart(2, '0');
      if (this.timer.minutes === 0 && this.timer.hours === 0) {
        return `${ss}`;
      }
      if (this.timer.hours === 0) {
        return `${mm}:${ss}`;
      } else {
        const hh = this.timer.hours.toString().padStart(2, '0');
        return `${hh}:${mm}:${ss}`;
      }
    }
  }
};
</script>

<style lang="scss" scoped>
.active {
  .timer-time {
    color: var(--white);
    border-color: var(--white);
  }

  .timer-controls-toggle-start {
    border-top: 10px solid transparent;
    border-bottom: 10px solid transparent;
    border-left: 17px solid var(--white);
    background: transparent;
  }

  .timer-controls-reset-icon {
    background: var(--white);
  }
}

.timer {
  background: var(--gray);
  height: 120px;
  max-width: 225px;
  width: 100%;
  max-height: 120px;
}

.timer-time,
.timer-controls {
  display: flex;
  justify-content: center;
  padding: 20px 0;
}

.timer-time {
  border-bottom: 1px solid var(--light-gray);
  color: var(--light-gray);
}

.timer-controls {
  gap: 40px;
}

.timer-controls-toggle {
  display: flex;
  cursor: pointer;
  max-width: 20px;
  width: 100%;
}

.timer-controls-toggle-start {
  display: inline-block;
  width: 0;
  height: 0;
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent;
  border-left: 17px solid var(--light-gray);
  background: transparent;
  transform: rotate(0deg);
  cursor: pointer;
}

.timer-controls-reset-icon {
  width: 18px;
  height: 18px;
  background: var(--light-gray);
  border: none;
  cursor: pointer;
}

.timer-controls-toggle-pause {
  display: flex;
  gap: 5px;
}

.timer-controls-toggle-pause-stripe {
  width: 3px;
  height: 20px;
  background-color: var(--white);
}

.timer-controls-reset {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

