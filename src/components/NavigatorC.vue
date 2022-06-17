<template>
  <section class="src-components-navigator">
    <div id="navigator">
      <button id="reset" @click="getReset()">{{ getMensaje(mensaje) }}</button>
      <span id="message">
        {{ mensaje }}
      </span>

      <button @click="hardToEasy()" :style="getBtn(!isHard)">easy</button>
      <button @click="easyTohard()" :style="getBtn(isHard)" class="selected">
        hard
      </button>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-components-navigator",
  props: ["mensaje", "reset"],
  mounted() {},
  data() {
    return { isHard: true };
  },
  methods: {
    hardToEasy() {
      this.isHard = false;
      this.$emit("isHard", false);
      this.$emit("numero", 3);
    },
    easyTohard() {
      this.isHard = true;
      this.$emit("isHard", true);
      this.$emit("numero", 6);
    },
    getBtn(isHard) {
      return {
        "background-color": isHard ? "steelblue" : "white",
        color: isHard ? "white" : "steelblue",
      };
    },
    getReset() {
      this.$emit("reset", true);
    },
    getMensaje(message) {
      return message != "You Picked Right!" ? "New colors" : "Play Again!";
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
#navigator {
  background: #ffffff;
  height: 30px;
  text-align: center;
  margin: 0;
  margin-top: -30px;
}
#message {
  color: black;
  display: inline-block;
  width: 20%;
}
.selected {
  background-color: steelblue;
  color: white;
}
button {
  border: none;
  background-color: white;
  font-family: "Montserrat", "Avenir";
  text-transform: uppercase;
  height: 100%;
  font-weight: 700;
  letter-spacing: 1px;
  color: steelblue;
  transition: all 0.3s;
  outline: none;
}
button:hover {
  color: white;
  background-color: steelblue;
}
</style>
