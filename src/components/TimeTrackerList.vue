<template>
  <div class="timers-container">
    <ul class="timers-list">
      <li class="timers-element" v-for="(timer, index) in timers" :key="timer.id">
        <Timer :timer="timer" @update-timer="(updatedTimer) => timers[index] = updatedTimer"/>
      </li>
      <li class="timers-element">
        <div class="timers-add" @click="addTimer">
          <span class="timers-add-plus"></span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import Timer from './TimeTracker.vue';
import {nanoid} from 'nanoid';

export default {
  name: 'TimerList',
  components: {
    Timer
  },
  data() {
    return {
      timers: [{
        id: nanoid(5),
        hours: 0,
        minutes: 0,
        seconds: 0
      }]
    }
  },
  methods: {
    addTimer() {
      this.timers.push({
        id: nanoid(5),
        hours: 0,
        minutes: 0,
        seconds: 0
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.timers-container {
  max-width: 830px;
  margin: 0 auto;
  padding: 0 50px;
}

.timers-list {
  padding: 70px 0;
  display: grid;
  justify-content: center;
  grid-template-columns: repeat(3, 1fr);
  gap: 50px;

  @media (min-width: 768px) and (max-width: 1023px) {
    grid-template-columns: repeat(2, 0.4fr);
  }

  @media (max-width: 767px) {
    grid-template-columns: repeat(1, 1fr);
  }
}

.timers-element {
  display: flex;
  justify-content: center;
}

.timers-add {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 120px;
  min-width: 225px;
  max-width: 225px;
  width: 100%;
  position: relative;
  cursor: pointer;
  background: var(--gray);

  &-plus:before,
  &-plus:after {
    content: "";
    position: absolute;
    width: 20px;
    height: 3px;
    top: calc(50% - 1px);
    left: calc(50% - 10px);
    background-color: var(--light-gray);
    transform: rotate(90deg);
  }

  &-plus:after {
    transform: rotate(180deg);
  }
}
</style>