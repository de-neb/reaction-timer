<template>
  <div class="block-cont" v-if="showBlock">
    <div class="block" @click="stopTimer" :class="generatePosition()">
      <h1>CLICK ME</h1>
    </div>
  </div>
</template>

<script>
export default {
  props: ["delay"],
  data() {
    return {
      time: null,
      timer: null,
      showBlock: false,
      position: [
        "top-right",
        "top-left",
        "bottom-right",
        "bottom-left",
        "top-center",
        "bottom-center",
        "middle",
        "middle-left",
        "middle-right",
      ],
    };
  },
  methods: {
    generatePosition() {
      let pos = Math.floor(Math.random() * this.position.length);
      return this.position[pos];
    },
    startTimer() {
      this.timer = setInterval(() => {
        this.time++;
      }, 1);
    },
    stopTimer() {
      clearInterval(this.timer);
      this.$emit("block-click", this.time);
    },
  },
  mounted() {
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay);
  },
};
</script>


<style>
hr {
  border: none;
  border-bottom: 5px double #7868e6;
}

.block {
  width: 350px;
  height: 350px;
  background: #7868e6;
  border-radius: 20px;
  margin: 0;
  color: #fff;
  display: grid;
  place-items: center;
  position: absolute;
}

@media (max-width: 900px) {
  .block {
    width: 250px;
    height: 250px;
  }
}

@media (max-width: 550px) {
  .block {
    width: 200px;
    height: 200px;
  }
}

.block-cont {
  margin: 30px 0;
  width: 95vw;
  height: 63vh;
  position: relative;
  left: 50%;
  transform: translate(-50%, 0);
}

.top-right {
  top: 0;
  left: 0%;
}

.top-left {
  top: 0;
  right: 0;
}

.top-center {
  top: 0;
  left: 50%;
  transform: translate(-50%, 0);
}

.bottom-left {
  bottom: 0;
  left: 0;
}

.bottom-right {
  bottom: 0;
  right: 0;
}

.bottom-center {
  bottom: 0;
  left: 50%;
  transform: translate(-50%, 0);
}

.middle {
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.middle-left {
  top: 50%;
  left: 0;
  transform: translate(0, -50%);
}

.middle-right {
  top: 50%;
  right: 0;
  transform: translate(0, -50%);
}
</style>
