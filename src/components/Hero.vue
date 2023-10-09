<template>
  <div class="flex flex-col items-center justify-center h-screen bg-gray-100">
    <div class="text-4xl font-bold mb-4">{{ minutes }}m : {{ formattedSeconds }}s</div>
    <div class="flex space-x-4">
      <button class="px-4 py-2 bg-blue-500 text-white rounded" @click="startTimer">Start</button>
      <button class="px-4 py-2 bg-blue-500 text-white rounded" @click="stopTimer">Stop</button>
      <button class="px-4 py-2 bg-blue-500 text-white rounded" @click="resetTimer">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      seconds: 0,
      minutes: 0,
      intervalId: null
    }
  },

  computed: {
    formattedSeconds() {
      // Pad the seconds value with leading zero
      return String(this.seconds).padStart(2, '0')
    }
  },

  methods: {
    startTimer() {
      if (!this.intervalId) {
        this.intervalId = setInterval(() => {
          this.seconds++
          if (this.seconds === 60) {
            this.minutes++
            this.seconds = 0
          }
        }, 1000)
      }
    },

    stopTimer() {
      clearInterval(this.intervalId)
      this.intervalId = null
    },

    resetTimer() {
      this.stopTimer()
      this.seconds = 0
      this.minutes = 0
    }
  }
}
</script>