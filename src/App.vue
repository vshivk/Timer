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

<style lang="scss">
:root {
  --dark: #353638;
  --white: #fff;
  --gray: #696969;
  --light-gray: #9E9E9E;
  --font: 'Gotham Pro', sans-serif;
}

@font-face {
  font-family: 'Gotham Pro';
  src: url('assets/fonts/gothampro.woff'), url('assets/fonts/gothampro.woff2'), url('assets/fonts/gothampro.ttf');
  font-weight: 400;
  font-style: normal;
}

body {
  font-family: var(--font);
  background-color: var(--dark);
}

ul {
  list-style-type: none;
  padding-inline-start: 0;
  margin: 0;
}
</style>
