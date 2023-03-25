<template>
  <div class="timers-container">
    <div class="timers-wrapper">
      <div class="timers-element" v-for="(timer, index) in timers" :key="index">
        <Timer :hours="timer.hours" :minutes="timer.minutes" :seconds="timer.seconds"/>
      </div>
      <div class="timers-element">
        <div class="timers-add" @click="addTimer">
          <span class="timers-add-cross"></span>
        </div>
      </div>
    </div>
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
<style scoped>
.timers-container {
  max-width: 830px;
  margin-left: auto;
  margin-right: auto;
  padding-left: 50px;
  padding-right: 50px;
}

.timers-wrapper {
  padding: 70px 0;
  display: grid;
  justify-content: center;
  grid-template-columns: repeat(3, 1fr);
  gap: 50px;
}

@media (min-width: 768px) and (max-width: 1023px) {
  .timers-wrapper {
    grid-template-columns: repeat(2, 0.4fr);
  }
}

@media (min-width: 320px) and (max-width: 767px) {
  .timers-wrapper {
    grid-template-columns: repeat(1, 1fr);
  }

  .timers-element {
    display: flex;
    justify-content: center;
  }
}

.timers-add {
  background: #696969;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 120px;
  min-width: 225px;
  max-width: 225px;
  width: 100%;
  position: relative;
  cursor: pointer;
}

.timers-add-cross:before, .timers-add-cross:after {
  content: "";
  position: absolute;
  width: 20px;
  height: 3px;
  top: calc(50% - 1px);
  left: calc(50% - 10px);
  background-color: #9E9E9E;
  transform: rotate(90deg);
}

.timers-add-cross:after {
  transform: rotate(180deg);
}


</style>