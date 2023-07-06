<template>
  <div class="stopwatch">
    <h1>Stopwatch</h1>
    <div class="time" :class="{ 'countdown': isRunning && elapsedTime > 0, 'green': !isRunning }">
      {{ formatTime(elapsedTime) }}
    </div>
    <div class="buttons">
      <button class="start-button" @click="startStopwatch" :disabled="isRunning">
        <span v-if="!isRunning">Start</span>
        <span v-else>Resume</span>
      </button>
      <button class="stop-button" @click="stopStopwatch" :disabled="!isRunning">Stop</button>
      <button class="reset-button" @click="resetStopwatch">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Stopwatch',
  data() {
    return {
      isRunning: false,
      startTime: null,
      elapsedTime: 0,
      timerInterval: null,
    };
  },
  methods: {
    startStopwatch() {
      if (!this.isRunning) {
        this.isRunning = true;
        this.startTime = Date.now() - this.elapsedTime;
        this.timerInterval = setInterval(() => {
          this.elapsedTime = Date.now() - this.startTime;
        }, 10);
      }
    },
    stopStopwatch() {
      if (this.isRunning) {
        this.isRunning = false;
        clearInterval(this.timerInterval);
      }
    },
    resetStopwatch() {
      this.isRunning = false;
      this.startTime = null;
      this.elapsedTime = 0;
      clearInterval(this.timerInterval);
    },
    formatTime(milliseconds) {
      const minutes = Math.floor(milliseconds / 60000);
      const seconds = Math.floor((milliseconds % 60000) / 1000);
      const centiseconds = Math.floor((milliseconds % 1000) / 10);
      return `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}.${centiseconds
        .toString()
        .padStart(2, '0')}`;
    },
  },
};
</script>

<style>
.stopwatch {
  text-align: center;
  margin-top: 50px;
  border: 6px solid rgb(61, 103, 60);
}

h1 {
  font-size: 40px;
  margin-bottom: 10px;
  color: rgb(61, 103, 60); /* Ubah warna tulisan menjadi hijau */
}

.time {
  font-size: 96px;
  font-weight: bold;
  margin: 20px 0;
  transition: color 0.3s ease;
  color: #00ff00; /* Ubah warna tulisan menjadi hijau */
}

.countdown {
  animation: countdownAnimation 1s infinite alternate;
  color: #dc3545;
}

.green {
  color: #00ff00; /* Ubah warna tulisan menjadi hijau */
}

@keyframes countdownAnimation {
  0% {
    transform: scale(1);
  }
  100% {
    transform: scale(1.2);
  }
}

.buttons {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-bottom: 60px;
}

button {
  padding: 10px 20px;
  font-size: 20px;
  border-radius: 5px;
  cursor: pointer;
  border: none;
  outline: none;
  transition: background-color 0.3s ease;
}

.start-button {
  background-color: #5c7f64;
  color: #fff;
}

.start-button:disabled {
  background-color: #12a41e;
  cursor: not-allowed;
}

.start-button:hover:not(:disabled) {
  background-color: #218838;
}

.stop-button {
  background-color: #008cff;
  color: #fff;
}

.stop-button:disabled {
  background-color: #30888f;
  cursor: not-allowed;
}

.stop-button:hover:not(:disabled) {
  background-color: #2805eb;
}

.reset-button {
  background-color: #da6e9b;
  color: #212529;
}

.reset-button:hover {
  background-color: #ff0191;
}
</style>
