<template>
  <div class="">
    <h1>{{ msg }}</h1>
    <p>{{ lambdaMsg }}</p>
    <p>
      <button @click="callLambda">Get Message from Lambda</button>
    </p>

  </div>

</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String
  },
  data() {
    return { lambdaMsg: "Click to get a message" };
  },
  methods: {
    callLambda() {
      fetch(
        "https://6dmd5ym6r1.execute-api.us-east-2.amazonaws.com/latest/rate?country=AU&weight=1000"
      )
        .then(response => response.json())
        .then(json => {
          this.lambdaMsg = json;
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
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
