<template>
  <img style="width: 200px" src="./../assets/Btc.png" />
  <h1>Bitcoin in Real Time</h1>

  <div>
    <h2>USD</h2>
    <span>$36,000.00</span>
  </div>

  <div>
    <h2>BRL</h2>
    <span>R$194,000.00</span>
  </div>

  <button v-on:click="timer">{{time}}</button>
</template>

<script>
export default {
  name: "BtcPrice",
  data() {
    return { time: 30 };
  },
  methods: {
    timer() {
      setInterval(() => {
          this.time--
          if (this.time < 0) {
              this.time = 30;
          }
      }, 1000);
    },
  },
  beforeMount() {
      this.timer();
  }
};


</script>