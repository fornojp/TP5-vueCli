<template>
  <section class="src-components-header">
    <div id="header" :style="bcgHeader()">
      <h1>
        The Great <br />
        <span id="colorDisplay">{{
          pickedColorHeader.style.backgroundColor
        }}</span>
        <br />
        Guessing Game
      </h1>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-components-header",
  props: ["pickedColorHeader", "mensaje"],
  mounted() {},
  data() {
    return {};
  },
  methods: {
    bcgHeader() {
      return {
        "background-color":
          this.mensaje != "You Picked Right!"
            ? "steelblue"
            : this.pickedColorHeader.style.backgroundColor,
      };
    },
  },
  computed: {},
};
</script>

<style scoped lang="css">
#header {
  transition: all 0.3s;
  background: steelblue;
  text-transform: uppercase;
  text-align: center;
  margin: 0;
  color: white;
}
#colorDisplay {
  font-size: 200%;
}
</style>
