<template>
  <div id="app">
    <b-container>
      <h1 class="header">Final Countdown</h1>
      <b-nav pills>
        <b-nav-item disabled>Take 5</b-nav-item>
        <b-nav-item disabled>10</b-nav-item>
        <b-nav-item disabled>20</b-nav-item>
        <b-nav-item disabled>30</b-nav-item>
        <b-nav-item disabled>60</b-nav-item>
        <b-nav-form @submit.prevent="alert('Form Submitted')">
          <b-form-input class="mr-1" placeholder="How many minutes?"></b-form-input>
          <b-button type="submit">Ok</b-button>
        </b-nav-form>
      </b-nav>
      <div class="timeLeft">10:00</div>
      <div class="endTime">Be right back!</div>
    </b-container>
  </div>
</template>

<script>

export default {
  name: 'App'
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

.header {
  color: black;
  text-shadow: 2px 2px 0 rgba(0, 0, 0, 0.5);
  margin-bottom: 30px;
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
}
.endTime {
  font-size: 2rem;
  color: black;
}
</style>
