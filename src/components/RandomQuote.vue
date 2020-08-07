<template>
  <div>
    <div class="header">
      <h1>{{ msg }}</h1>
    </div>
    <div class="quote">
      <h2 v-if="quotes[0]">
        {{ quotes[0].text }}
      </h2>
    </div>
    <b-button
      type="is-info"
      size="is-large"
      rounded
      inverted
      :loading="loading"
      :disabled="loading"
      @click="generateQuote"
      >Generate Random Quote</b-button
    >
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'RandomQuote',
  props: {
    msg: String,
  },
  data() {
    return {
      quotes: [],
      loading: false,
    };
  },

  mounted() {
    this.generateQuote();
  },

  methods: {
    shuffle(arr) {
      return arr.sort(() => 0.5 - Math.random());
    },
    generateQuote() {
      this.loading = true;
      axios
        .get('https://type.fit/api/quotes')
        .then((result) => {
          this.quotes = this.shuffle(result.data);
          this.loading = false;
        })
        .catch((error) => {
          console.log(error);
          this.loading = false;
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.header {
  font-size: 3rem;
  color: white;
  text-shadow: 2px 2px black;
}
.quote {
  font-size: 2rem;
  color: white;
  text-shadow: 2px 2px black;
  display: flex;
  align-items: center;
  flex-direction: column;
  margin-top: 2rem;
  height: 12rem;
  * {
    max-width: 700px;
  }
}
body {
  background-image: url('https://wallpapercave.com/wp/l9WDprr.jpg');
  background-repeat: no-repeat;
  background-size: cover;
}

#app {
  button {
    margin-top: 2rem;
  }
  .button.is-info.is-loading::after {
    border-color: transparent transparent skyblue skyblue !important;
  }
}
</style>
