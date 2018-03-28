<template>
  <div class="">
    <h1>{{ msg }}</h1>
    <p>{{ lambdaMsg }}</p>
    <div>
      <label>
        Country (ISO-2)
        <input type="text" v-model="country">
      </label>
    </div>
    <div>
      <label>
        Weight (grams)
        <input type="text" v-model="grams">
      </label>
    </div>
    <p>
      <button @click="callLambda">Get Rates from Lambda</button>
    </p>

    <table>
      <tr>
        <th>Country</th>
        <th>Method</th>
        <th>Rate</th>
        <th>minWeight</th>
        <th>maxWeight</th>
      </tr>
      <tr v-for="rate in shippingRates" :key="rate.method">
        <td>{{rate.countryNameEnglish}}</td>
        <td>{{rate.method}}</td>
        <td>{{rate.rate}}</td>
        <td>{{rate.minWeight}}</td>
        <td>{{rate.maxWeight}}</td>
      </tr>
    </table>

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
      country: "tr",
      grams: "500",
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
