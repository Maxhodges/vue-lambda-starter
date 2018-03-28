<template>
  <div class="">
    <h1>{{ msg }}</h1>
    <p>{{ lambdaMsg }}</p>
    <label>
      Country (ISO-2)
      <input type="text" v-model="country">
    </label>
    <label>
      Weight (grams)
      <input type="text" v-model="grams">
    </label>
    <p>
      <button @click="callLambda">Get Message from Lambda</button>
    </p>
    <ul>
      <li v-for="rate in shippingRates" :key="rate.method">{{rate.countryNameEnglish}} {{rate.method}} Rate={{rate.rate}} JPY MinWeight={{rate.minWeight}}, MaxWeight={{rate.maxWeight}}</li><br>
    </ul>

  </div>

</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return {
      lambdaMsg: "Click to get a message",
      country: "",
      grams: "",
      shippingRates: []
    };
  },
  methods: {
    callLambda() {
      fetch(
        `https://6dmd5ym6r1.execute-api.us-east-2.amazonaws.com/latest/rate?country=${this.country.toUpperCase()}&weight=${
          this.grams
        }`
      )
        .then(response => response.json())
        .then(json => {
          this.shippingRates = json;
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}

a {
  color: #42b983;
}
</style>
