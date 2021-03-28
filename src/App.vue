<template>
  <h1>REACTION TIMER</h1>
  <h4>
    Quickly click for the box that will randomly pop out in any position below
    the line.
  </h4>
  <button @click="start" :disabled="isPlaying" class="play">Play</button>
  <Results v-if="isDone" :time="time" />
  <hr />
  <Block v-if="isPlaying" @block-click="end" :delay="delay" />
</template>

<script>
import Block from "./components/Block";
import Results from "./components/Results";

export default {
  name: "App",
  data() {
    return {
      isPlaying: false,
      isDone: false,
      delay: null,
      time: null,
    };
  },
  methods: {
    start() {
      this.delay = 2000 + Math.floor(Math.random() * 6000);
      this.isPlaying = true;
      this.isDone = false;
    },
    end(time) {
      this.time = time;
      this.isPlaying = false;
      this.isDone = true;
    },
  },
  components: {
    Block,
    Results,
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Encode+Sans+Condensed:wght@400;700&family=Roboto&display=swap");

body {
  margin: 0;
  font-family: "Roboto", sans-serif;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 80px;
}

h1 {
  font-size: 2.5rem;
  font-weight: 600;
  font-family: "Encode Sans Condensed", sans-serif;
}

.play {
  width: 100px;
  height: auto;
  padding: 10px 5px;
  font-size: 1.3rem;
  background: #7868e6;
  color: #fff;
  border-radius: 5px;
  cursor: pointer;
  border: none;
  margin: 15px auto;
}

.play:hover {
  background: rgb(82, 71, 158);
}

.play:disabled {
  background: rgb(179, 171, 230);
  cursor: not-allowed;
}
</style>
