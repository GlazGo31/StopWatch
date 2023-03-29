<template>
  <div class="app">
    <div class="timer" :class="{'change-color': isActivePlay}">{{ `${timerDate.hours > 9 ?`${timerDate.hours}`:`0${timerDate.hours}`}:
${timerDate.minutes > 9 ?`${timerDate.minutes}`:`0${timerDate.minutes}`}:
${timerDate.second>9 ?`${timerDate.second}`:`0${timerDate.second}`}`}}
    </div>
    <div class="timer__btn">
      <button @click="start" class="click-start" :class="{'active-play': isActivePlay}">
        <img src="../image/play.png" alt="play" class="click-start__images">

      </button>
      <button  @click='pause' class="click-stop" :class="{'active-stop': isActivePlay}">
        ||
      </button>
      <button  class="click-reset" @click="reset" :class="{'active-reset': isActivePlay}">
        <div class="click-reset__images"></div>
      </button>
    </div>
  </div>
</template>

<script>

export default {
  name: "v-Watch",
  components: {},
  data() {
    return {
      timerDate: {
        hours: 0,
        minutes: 0,
        second: 0
      },
      timeOutId: null,
      timeOutCount: null,
      isActivePlay: false
    }
  },
  computed: {},
  methods: {
    start() {
      const componentDataContext = this
      const {timerDate} = this
      this.isActivePlay = true

      if (timerDate.second < 59) {

        componentDataContext.timeOutId = setTimeout(function run() {
          timerDate.second++
          if(timerDate.second > 59) {
            timerDate.minutes += 1
            timerDate.second = 0

            if(timerDate.minutes > 59) {
              timerDate.minutes = 0
              timerDate.hours += 1
            }

          }
          componentDataContext.timeOutCount = setTimeout(run, 1000)
        }, 0)
      }
    },

    pause() {
      this.isActivePlay = false
      clearTimeout(this.timeOutCount)
      clearTimeout(this.timeOutId)
    },

    reset() {
      clearTimeout(this.timeOutCount)
      clearTimeout(this.timeOutId)
      this.isActivePlay = false
      this.timerDate.hours = 0;
      this.timerDate.minutes = 0;
      this.timerDate.second = 0
    }
  },
}
</script>
