<template>
  <h1>Ninja Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">Play</button>

  <Block v-if="isPlaying" :delay="delay" :isPlaying="isPlaying" @end="endGame"/>
  <div>
    <Results v-if="score" :score="score"/>
  </div>
</template>

<script>
import Block from './components/Block.vue';
import Results from './components/Results.vue';

export default {
  name: 'App',
  components: {
    Block,
    Results
},
  data() {
    return {
      isPlaying: false,
      delay: null,
      score: null,
    }
  },
  methods: {
    start() {
      if(this.isPlaying) return;
      this.delay = 2000 + Math.random() * 5000;
      this.isPlaying = true;
      this.score = null;
    },
    endGame (reactionTime) {
      this.isPlaying = false;
      this.score = reactionTime;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
button {
        color: #fff;
        background: #0faf87;
        border: none;
        padding: 8px 16px;
        border-radius: 4px;
        font-size: 16px;
        letter-spacing: 1px;
        cursor: pointer;
        margin: 10px;
    }

    button[disabled] {
        opacity: 0.2;
        cursor: not-allowed;
    }
</style>
