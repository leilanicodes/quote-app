<template>
  <div class="background">
    <div class="e-container">
      <h2 class="quote" v-if="quotes[0] && quotes[0].author !== 'Donald Trump'">
        {{ quotes[0].text }}
      </h2>
      <h2 v-else>
        Better than a thousand hollow words is one word that brings peace.
      </h2>
      <div class="author">
        <h3
          v-if="
            quotes[0] && quotes[0].author && quotes[0].author !== 'Donald Trump'
          "
        >
          - {{ quotes[0].author }}
        </h3>
        <h3 v-else-if="quotes[0].author === 'Donald Trump'">-Buddha</h3>
        <h3 v-else>- Unknown</h3>
      </div>
    </div>
    <b-button
      type="is-info"
      size="is-large"
      rounded
      inverted
      :loading="loading"
      :disabled="loading"
      @click="handleClick"
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
    // this.changeBackground('https://source.unsplash.com/1600x900/?nature');
    this.changeBackground();
  },

  methods: {
    shuffle(arr) {
      return arr.sort(() => 0.5 - Math.random());
    },
    handleClick() {
      this.generateQuote();

      this.changeBackground();
    },
    generateQuote() {
      this.loading = true;
      axios
        .get('https://type.fit/api/quotes')
        .then((result) => {
          this.quotes = this.shuffle(result.data);
          console.log(this.quotes);
          this.loading = false;
        })
        .catch((error) => {
          console.log(error);
          this.loading = false;
        });
    },
    changeBackground() {
      // axios
      //   .get('https://picsum.photos/v2/list?page=1&limit=10')
      //   .then((result) => {
      //     console.log(result);
      //     this.image = this.shuffle(result.data);
      //     console.log('image', this.image[0].url);
      //   });

      function randomHSL() {
        return 'hsla(' + ~~(360 * Math.random()) + ',' + '70%,' + '80%,1)';
      }
      document.body.style.backgroundColor = randomHSL();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.e-container {
  font-size: 2rem;
  color: black;
  padding: 2rem;
  // width: 50rem;
  width: 80vw;
  max-width: 800px;
  margin-top: 2rem;
  border-radius: 3rem;
  display: flex;
  justify-content: space-between;
  flex-direction: column;

  height: 25rem;
  background-color: #ffffffb3;

  .quote {
    margin-top: 1rem;
    margin-left: 1rem;
    padding-right: 2rem;
    text-align: left;
    align-self: flex-start;
    font-family: 'Noto Sans TC', sans-serif;
    font-size: 2rem;
    width: 100%;
  }
  .author {
    font-family: cursive;
    text-align: right;
    font-size: 2.2rem;
    padding-right: 2rem;
  }
}
.background {
  // background-image: url('https://wallpapercave.com/wp/l9WDprr.jpg');
  // background-repeat: no-repeat;
  // background-size: cover;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
body {
  transition: background-color 0.5s ease;
}
#app {
  button {
    margin-top: 2rem;
    color: black;
    background-color: #ffffffb3;
    width: 20rem;
    font-family: 'Noto Sans TC', sans-serif;
    font-size: 1.5rem;
  }
  button:hover {
    background-color: #ffffffe3;
  }
  .button.is-info.is-loading::after {
    border-color: transparent transparent skyblue skyblue !important;
  }
}

@media only screen and (max-width: 414px) {
  .e-container {
    height: 80vh;
    width: 95vw;
    margin-top: 0.5rem;
    .quote {
      font-size: 1.6rem;
    }
    .author {
      font-size: 1.6rem;
    }
  }
}
</style>
