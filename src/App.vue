<template>
  <div id="app">
    <b-container>
      <div class="main-content">
        <h1 class="header">Final Countdown</h1>
        <b-nav pills>
          <b-nav-item @click="timer(300)">Take 5</b-nav-item>
          <b-nav-item @click="timer(600)">10</b-nav-item>
          <b-nav-item @click="timer(1200)">20</b-nav-item>
          <b-nav-item @click="timer(1800)">30</b-nav-item>
          <b-nav-item @click="timer(3600)">60</b-nav-item>
          <b-nav-form @submit.prevent="customTimer()">
            <b-form-input class="mr-1" v-model="minutes" placeholder="How many minutes?"></b-form-input>
            <b-button type="submit">Ok</b-button>
          </b-nav-form>
        </b-nav>
        <div class="timeLeft">{{ timeLeft || 'Take a Break :)' }}</div>
        <div class="endTime">{{ endTime }}</div>
      </div>
    </b-container>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      timeLeft: '',
      endTime: '',
      countdown: null,
      minutes: null
    }
  },
  methods: {
    getTimeLeft(seconds) {
      let secondsLeft = seconds
      const minutes = Math.floor(secondsLeft / 60)
      secondsLeft %= 60
      this.timeLeft = `${minutes < 10 ? '0' : ''}${minutes}:${secondsLeft < 10 ? '0' : ''}${secondsLeft}`
    },
    getEndTime(then) {
      const x = new Date(then)
      const hours = x.getHours()
      const minutes = x.getMinutes()
      this.endTime = `Be right back at ${hours < 10 ? '0' : ''}${hours}:${minutes < 10 ? '0' : ''}${minutes}!`
    },
    timer(seconds) {
      clearInterval(this.countdown)

      const now = Date.now()
      const then = now + seconds * 1000
      this.getTimeLeft(seconds)
      this.getEndTime(then)

      this.countdown = setInterval(() => {
        const newNow = Math.round((then - Date.now()) / 1000)
        if(newNow < 0) {
          console.log('THE END')
          clearInterval(this.countdown)
        } else {
          this.getTimeLeft(newNow)
        }
      }, 1000)
    },
    customTimer() {
      console.log(this.minutes)
      const x = parseFloat(this.minutes)
      this.timer(x * 60)
      this.minutes = null
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
  min-height: 100vh;
  background: linear-gradient(lightblue, red);
}

.main-content {
  border: 3px solid blue;
  border-radius: 5px;
  background: rgba(255, 255, 255, 50%);
  box-shadow: 5px 5px 2px rgba(0, 0, 0, 0.5);
}

.header {
  color: black;
  text-shadow: 2px 2px 0 rgba(0, 0, 0, 0.5);
  margin-bottom: 30px;
  border-bottom: 1px solid grey;
}

.nav-item {
  flex: 1;
  color: black;
  border-right: 1px dotted black;
}

.nav-item > a {color: black !important;}

.nav-item:hover {
  cursor: pointer;
  background-color: hsla(0, 100%, 50%, 0.5);
  font-weight: bold;
  border-radius: 15px;
  box-shadow: 0 2px 2px black;
}

.timeLeft {
  font-size: 150px;
  color: black;
  transition: all 2s;
}
.endTime {
  font-size: 2rem;
  color: black;
}
</style>
