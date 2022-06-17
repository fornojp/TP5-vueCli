<template>
  <section class="src-components-container">
    <div id="container" v-for="(color, index) in colors" :key="index">
      <div
        class="square"
        :style="getFondo(color.style.backgroundColor)"
        @click="getColor(color)"
      >
        {{ color.style.backgroundColor }}
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-components-container",
  components: {},
  props: ["colors", "pickedColor", "reset"],
  data() {
    return {
      mensajeDisplay: "",
    };
  },

  methods: {
    getColor(color) {
      if (this.pickedColor === color) {
        this.mensajeDisplay = "You Picked Right!";
      } else {
        this.mensajeDisplay = "Try Again!";
        color.style.backgroundColor = "#232323";
      }
      this.$emit("mensajeDisplay", this.mensajeDisplay);
    },
    getFondo(color) {
      return {
        "background-color":
          this.mensajeDisplay === "You Picked Right!"
            ? this.pickedColor.style.backgroundColor
            : color,
      };
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
#container {
  margin: 20px auto;
  max-width: 600px;
}
.square {
  width: 30%;
  background: blue;
  padding-bottom: 30%;
  float: left;
  margin: 1.66%;
  border-radius: 10%;
  transition: background 0.8s;
  -webkit-transition: background 0.8s;
  -moz-transition: background 0.8s;
}
</style>
