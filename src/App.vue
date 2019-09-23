<template>
  <div id="app">
    <div class="quote">
      <h1>{{ currentQuote }}</h1>
      <h2>{{ currentAuthor }}</h2>
      <button @click="getRandomQuote">Random Quote</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "app",
  data() {
    return {
      quotesData: null,
      randomQuote: null,
      currentQuote: null,
      currentAuthor: null
    };
  },
  methods: {
    getRandomQuote() {
      this.randomQuote = this.quotesData.data.quotes[
        Math.floor(Math.random() * this.quotesData.data.quotes.length)
      ];

      this.currentQuote = this.randomQuote.quote;
      this.currentAuthor = this.randomQuote.author;
    }
  },
  mounted() {
    axios
      .get(
        "https://gist.githubusercontent.com/camperbot/5a022b72e96c4c9585c32bf6a75f62d9/raw/e3c6895ce42069f0ee7e991229064f167fe8ccdc/quotes.json"
      )
      .then(response => (this.quotesData = response));
  }
};
</script>

<style>
</style>
