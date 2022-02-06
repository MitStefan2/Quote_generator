<template>
  <div class="app">
    <Header title="The Anime Quoter" />
    <Quote :quote="quote" />
    <div class="button-container">
      <button @click="getQuote()">Get Quote</button>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Quote from "./components/Quote.vue";

export default {
  name: "App",
  components: {
    Header,
    Quote,
  },
  data() {
    return {
      quote: {},
      quotes: [],
    };
  },

  methods: {
    async getQuote() {
      const data = await fetch("https://api.quotable.io/random").then((res) =>
        res.json()
      );

      this.quote = {
        content: data.content,
        author: data.author,
      };
    },
  },
  created() {
    this.getQuote();
  },
};
</script>

<style lang="scss">
:root {
  --primary: #9E3536;
  --secondary: rgb(81, 40, 128);
  --tertiary: #32CBFF;
  --dark: rgb(143, 48, 50);
  --light: #EEE;
  --grey: #3F3F3F;
  --back: rgb(54, 52, 54);
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Open Sans", sans-serif;
  font-family: "Roboto Mono", monospace;
}
body {
  background-color: var(--back);
}
.button-container {
  display: flex;
  justify-content: center;
  padding: 0px 32px;
  margin: 64px auto;
}
button {
  border: none;
  outline: none;
  background-color: var(--primary);
  padding: 16px 32px;
  border-radius: 99px;
  color: var(--light);
  font-size: 28px;
  font-weight: 700;
  text-transform: uppercase;
  cursor: pointer;
  transition: 0.4s;

  &:hover {
    background-color: var(--secondary);
  }
}
</style>
