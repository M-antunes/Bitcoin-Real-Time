<template>
  <img style="width: 200px" src="./../assets/Btc.png" />
  <h1>Bitcoin in Real Time</h1>

  <div class="usd">
    <h2 >USD</h2>
    <span>${{ btcUsd }}</span>
  </div>

  <div class='brl'>
    <h2>BRL</h2>
    <span>${{ btcBrl }}</span>
  </div>

  <div >
   <h5>It'll respawn in: </h5>
  <h3 class="time"> {{ time }} </h3>
  </div>
</template>

<script>
export default {
  name: "BtcPrice",
  data() {
    return {
      time: 30,
      btcBrl: 0,
      btcUsd: 0,
    };
  },
  methods: {
    timer() {
      setInterval(() => {
        this.time--;
        if (this.time < 0) {
          this.time = 30;
          this.fetchPrices();
        }
      }, 1000);
    },

    async fetchPrices() {
      await fetch(`https://economia.awesomeapi.com.br/json/last/BTC-BRL,BTC-USD`)
        .then((response) => response.json())
        .then((data) => {
          this.btcBrl = data["BTCBRL"]["high"];
          this.btcUsd = data["BTCUSD"]["high"];
        })
      .catch((error) => console.log(`Error to fetch data: ${error}`));
    },
  },
  created() {
    this.fetchPrices();
  },
  beforeMount() {
    this.timer();
  },
};
</script>


