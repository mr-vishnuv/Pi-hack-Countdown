<template>
    <div class="countdown-container">
      <!-- Event Logo -->
      <img src="@/assets/logo.png" alt="Event Logo" class="event-logo" />
    
      <!-- Countdown Timer -->
      <div v-if="isTimerStarted" class="timer" @click="toggleTimer">
        {{ countdown }}
      </div>
  
      <!-- Start Button (Visible before starting the timer) -->
      <button v-if="!isTimerStarted" @click="startTimer" class="start-button">
        Start Timer
      </button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        countdown: '', // Countdown time display
        timerInterval: null, // Timer interval
        eventStartTime: null, // Event start time
        eventDuration: 24 * 60 * 60 * 1000, // Duration of the event (24 hours)
        targetTime: null, // Target time (when event ends)
        isTimerStarted: false, // Flag to check if the timer has started
        isPaused: false, // Flag to track if the timer is paused
      };
    },
    methods: {
      // Start the countdown timer
      startTimer() {
        this.isTimerStarted = true; // Mark timer as started
        this.eventStartTime = new Date().getTime(); // Set current time as the event start time
        this.targetTime = this.eventStartTime + this.eventDuration; // Set the target time for the event's end
        
        // Start the countdown
        this.timerInterval = setInterval(() => {
          this.updateCountdown();
        }, 1000);
      },
      
      // Update the countdown timer
      updateCountdown() {
        const currentTime = new Date().getTime();
        const timeLeft = this.targetTime - currentTime;
  
        if (timeLeft <= 0) {
          clearInterval(this.timerInterval); // Stop the timer when the event ends
          this.countdown = 'Event Ended!';
        } else {
          const hours = String(Math.floor(timeLeft / (1000 * 60 * 60))).padStart(2, '0');
          const minutes = String(Math.floor((timeLeft % (1000 * 60 * 60)) / (1000 * 60))).padStart(2, '0');
          const seconds = String(Math.floor((timeLeft % (1000 * 60)) / 1000)).padStart(2, '0');
          this.countdown = `${hours}:${minutes}:${seconds}`;
        }
      },
  
      // Toggle between pause and resume on click
      toggleTimer() {
        if (this.isPaused) {
          this.resumeTimer();
        } else {
          this.pauseTimer();
        }
      },
      
      // Pause the countdown timer
      pauseTimer() {
        clearInterval(this.timerInterval); // Stop the countdown interval
        this.isPaused = true; // Set the paused flag
      },
      
      // Resume the countdown timer
      resumeTimer() {
        this.timerInterval = setInterval(() => {
          this.updateCountdown();
        }, 1000); // Resume countdown
        this.isPaused = false; // Set the paused flag to false
      },
    },
  };
  </script>
  
  <style scoped>
  .countdown-container {
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    position: relative;
  }
  
  .event-logo {
    max-width: 500px;
    margin-bottom: 1rem;
  }
  
  .timer {
    font-size: 6rem; /* Increased size for the timer */
    font-weight: bold;
    letter-spacing: 0.1em;
    background: rgba(86, 34, 99, 0.767); /* Glow violet */
    padding: 2rem 3rem; /* Adjusted padding for larger font */
    border-radius: 10px;
    box-shadow: 0px 0px 20px rgba(188, 24, 230, 0.767); /* Glow effect */
    text-align: center;
    margin-bottom: 2rem;
    cursor: pointer;
  }
  
  .start-button {
    padding: 0.5em .7rem;
    font-size: 0.5rem;
    background-color: rgba(188, 24, 230, 0.7);
    color: rgb(82, 18, 78);
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .start-button:hover {
    background-color: rgba(188, 24, 230, 1);
  }
  </style>
  