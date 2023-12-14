<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <div id="app">
    <h1>Countdown app</h1>
    <label>Set Countdown (in seconds)</label>
    <input type="number" id="duration" v-model="duration" min="1" />
    <button @click="startCountdown()" :disabled="counting">Start</button>

    <div v-if="counting">
      <h2>Time remaining</h2>
      <p> {{ hours }} : {{ minutes }} : {{ seconds }}</p>
    </div>

    <div>
      <h2 v-if="countdownComplete">Countdown complete</h2>
    </div>

  </div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
      duration: 0,
      counting: false,
      hours: 0,
      minutes: 0,
      seconds: 0,
      countdownComplete: false,
      intervalid: null,
    }
  },
  methods: {
    startCountdown() {
      if (this.duration > 0 && !this.counting) {
        this.counting = true;
        this.intervalid = setInterval(() => {
          if (this.duration > 0) {
            this.duration--;
            this.calculateTime();
          }
          else {
            clearInterval(this.intervalid);
            this.counting = false;
            this.countdownComplete = true;
          }
        }, 1000)
      }
    },
    calculateTime() {
      this.hours = Math.floor(this.duration / 3600);
      this.minutes = Math.floor(this.duration / 60);
      this.seconds = this.duration % 60;
    }
  }
}

</script>

<style>
*{
  justify-content: center;
  text-align: center;
  padding: 5px;
  margin: 5px;
}
h2{
  color: red;
}
p{
  color: aqua;
}
button{
  background-color: chartreuse;
}
button:hover{
  cursor: pointer;
}

</style>

