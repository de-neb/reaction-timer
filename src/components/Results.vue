<template>
  <div class="results-cont">
    <p>Reaction Time :</p>
    <p>{{ time<1000 ? time:seconds }} {{ unit }}</p>
    <h3>{{ speed }}</h3>
  </div>
</template>

<script>
export default {
  props: ["time"],
  data() {
    return {
      speed: "Slow",
      unit: "ms",
      seconds: 0
    };
  },
  methods: {
    scoring(t) {
      this.unit = "ms";
      if (t <= 60) {
        this.speed = "Pretty good!";
      } else if (t <= 100) {
        this.speed = "Not bad";
      } else if (t <= 140) {
        this.speed = "You're slow";
      } else if (t <= 180) {
        this.speed = "Can't you click faster?";
      } else if (t <= 220) {
        this.speed = "Please react quickly";
      } else if (t < 1000) {
        this.speed = "Are you sleeping?";
      } else if (t >= 1000) {
        this.seconds = Math.round(t / 1000);
        this.unit = "s";
        this.speed = "Oh god, seriously?"
      }
    },
  },
  mounted() {
    this.scoring(this.time);
    console.log("success");
  },
};
</script>
    
<style>
.results-cont p {
  display: inline-block;
  margin-right: 20px;
  font-size: 1.4rem;
  font-weight: light;
}

.results-cont h3 {
  font-size: 2rem;
  margin: 0;
  color: #7868e6;
}
</style>