<template>
  <TimerList/>
</template>

<script>
import TimerList from "@/components/TimeTrackerList";

export default {
  name: 'App',
  components: {
    TimerList,
  }
}
</script>

<style>
@font-face {
  font-family: 'Gotham Pro';
  src: url('assets/fonts/gothampro.woff'), url('assets/fonts/gothampro.woff2'), url('assets/fonts/gothampro.ttf');
  font-weight: 400;
  font-style: normal;
}

body {
  font-family: 'Gotham Pro', sans-serif;
  background-color: #353638;
}

</style>
