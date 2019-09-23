<template>
  <div id="app" v-bind:style="{ backgroundColor: color}">
    <div class="quote-box" v-bind:style="{ color: color}">
      <div class="quote-text">
        <h1>
          <i class="fa fa-quote-left"></i>
          {{ currentQuote }}
        </h1>
      </div>
      <div class="quote-author">
        <h2>- {{ currentAuthor }}</h2>
      </div>
      <div class="buttons">
        <div class="social-buttons" v-bind:style="{ color: color}">
          <button class="button" @click="getRandomQuote" v-bind:style="{ backgroundColor: color}">
            <i class="fa fa-twitter"></i>
          </button>
          <button class="button" @click="getRandomQuote" v-bind:style="{ backgroundColor: color}">
            <i class="fa fa-tumblr"></i>
          </button>
        </div>
        <div class="new-button">
          <button
            class="button"
            @click="getRandomQuote"
            v-bind:style="{ backgroundColor: color}"
          >New Quote</button>
        </div>
      </div>
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
      currentAuthor: null,
      color: null,
      backgroundColors: [
        "#16a085",
        "#27ae60",
        "#2c3e50",
        "#f39c12",
        "#e74c3c",
        "#9b59b6",
        "#FB6964",
        "#342224",
        "#472E32",
        "#BDBB99",
        "#77B1A9",
        "#73A857"
      ]
    };
  },
  methods: {
    getRandomQuote() {
      this.randomQuote = this.quotesData.data.quotes[
        Math.floor(Math.random() * this.quotesData.data.quotes.length)
      ];

      this.color = this.backgroundColors[
        Math.floor(Math.random() * this.backgroundColors.length)
      ];

      this.currentQuote = this.randomQuote.quote;
      this.currentAuthor = this.randomQuote.author;
    }
  },
  created() {
    axios
      .get(
        "https://gist.githubusercontent.com/camperbot/5a022b72e96c4c9585c32bf6a75f62d9/raw/e3c6895ce42069f0ee7e991229064f167fe8ccdc/quotes.json"
      )
      .then(response => {
        this.quotesData = response;
        this.getRandomQuote();
      });
  }
};
</script>

<style>
body {
  margin: 0;
  font-family: "Roboto", sans-serif;
}

#app {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: orange;
}

.quote-box {
  max-width: 550px;
  border-radius: 5px;
  padding: 40px 50px;
  background-color: #fff;
  box-sizing: border-box;
}

.quote-author {
  text-align: right;
}

.buttons {
  display: flex;
  justify-content: space-between;
}

.button {
  height: 38px;
  background-color: orange;
  border-radius: 3px;
  border: none;
  color: #fff;
}

.social-buttons button {
  width: 40px;
  margin-right: 5px;
  font-size: 1.2em;
}

.new-button button {
  font-size: 0.9em;
}
</style>
