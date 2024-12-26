<template>
  <div id="app">
    <!-- Countdown Timer Component -->
    <CountdownTimer />
  </div>
</template>

<script>
import CountdownTimer from './components/CountdownTimer.vue';

export default {
  components: {
    CountdownTimer,
  },
};
</script>

<style>
/* Global styles for the app */
html, body, #app {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background: url('@/assets/1.png') no-repeat center center fixed;
  background-size: cover;
}

body::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5); /* Dark overlay for readability */
  z-index: -1; /* Ensure it doesn’t cover your content */
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  color: #e0b3ff;
  font-family: Arial, sans-serif;
}
</style>
