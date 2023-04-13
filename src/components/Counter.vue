<template id="app">
  <div>
    <section class="text-3xl flex justify-center content-center flex-col mx-auto text-center">
      <h3 v-if="!expired">Sắp đến tết rồi chỉ còn...</h3>
      <h3 v-else>Happy New Year</h3>
    </section>
    <section class="flex text-6xl justify-center content-center">
      <div class="days mr-2 relative">
        {{ displayDays  }}
        <div class="label text-sm absolute bottom-0">days</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="hours mx-2 relative">
        {{ displayHours  }}
        <div class="label text-sm absolute bottom-0">hours</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="minutes mx-2 relative">
        {{ displayMinutes }}
        <div class="label text-sm absolute bottom-0">minutes</div>
      </div>
      <span class="leading-snug">:</span>
      <div class="second ml-2 relative">
        <div>{{ displaySeconds }}
          <div class="label text-sm absolute bottom-0">seconds</div>
        </div>
      </div>
    </section>
  </div>
</template>
<script>
export default {
  name: 'Counter-view',
  data () {
    return {
      displayDays: 0,
      displayHours: 0,
      displayMinutes: 0,
      displaySeconds: 0,
      expired: false
    }
  },
  computed: {
    _seconds: () => 1000,
    _minutes () {
      return this._seconds * 60
    },
    _hours () {
      return this._minutes * 60
    },
    _days () {
      return this._hours * 24
    }
  },
  mounted () {
    this.showRemaining()
  },
  methods: {
    formatNum: num => (num < 10 ? '0' + num : num),
    showRemaining () {
      const timer = setInterval(() => {
        const now = new Date()
        const end = new Date(2024, 1, 10, 0, 0, 0, 0)
        const distance = end.getTime() - now.getTime()
        if (distance < 0) {
          clearInterval(timer)
          this.expired = true
          return
        }
        const days = Math.floor(distance / this._days)
        const hours = Math.floor((distance % this._days) / this._hours)
        const minutes = Math.floor((distance % this._hours) / this._minutes)
        const seconds = Math.floor((distance % this._minutes) / this._seconds)

        this.displayMinutes = this.formatNum(minutes)
        this.displaySeconds = this.formatNum(seconds)
        this.displayHours = this.formatNum(hours)
        this.displayDays = this.formatNum(days)
      }, 1000)
    }
  }
}
</script>
<style>
  .leading-snug {
    margin-top: -10px;
  }
  .app {
    background-image: '';
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
  }
</style>
