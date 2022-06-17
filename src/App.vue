<template>
  <div id="app">
    <Header
      :pickedColorHeader="this.colorHeaderVar"
      :mensaje="mensajeDisplay"
    />
    <Navigator
      @isHard="isHardNavigator = $event"
      @numero="colorCount = $event"
      :mensaje="mensajeDisplay"
      @reset="jugarDeNuevo = $event"
    />
    <Container
      :ishardContainer="isHardNavigator"
      :colors="colors"
      :pickedColor="colorHeaderVar"
      @mensajeDisplay="mensajeDisplay = $event"
      :reset="resetColores"
    />
    <p>{{ this.jugarDeNuevo }}</p>
  </div>
</template>

<script>
import Container from "./components/ContainerC.vue";
import Header from "./components/HeaderC.vue";
import Navigator from "./components/NavigatorC.vue";

export default {
  name: "App",
  components: {
    Container,
    Header,
    Navigator,
  },
  data() {
    return {
      isHardNavigator: true,
      colors: [],
      colorCount: 6,
      mensajeDisplay: "",
      colorHeaderVar: "",
      jugarDeNuevo: false,
      resetColores: false,
    };
  },
  created() {
    this.init();
    this.colorHeader();
  },
  beforeUpdate() {
    this.reset(this.jugarDeNuevo);
  },
  updated() {
    this.setColor();
  },
  methods: {
    init() {
      this.colors =
        this.colorCount == 6
          ? this.createNewColors(this.colorCount)
          : this.createNewColors(this.colorCount);
    },
    reset(jugarDeNuevo) {
      if (jugarDeNuevo) {
        this.colors = [];
        this.setColor();
        this.init();
        this.colorHeader();
        this.mensajeDisplay = "";
        this.jugarDeNuevo = false;
        this.resetColores = true;
      }
    },
    setColor() {
      if (this.colors.length != this.colorCount) {
        this.colors = this.createNewColors(this.colorCount);
        this.colorHeader();
      }
    },
    colorHeader() {
      this.colorHeaderVar = this.colors[this.PickColor()];
    },
    PickColor() {
      var quantity;
      if (this.isHardNavigator) {
        quantity = 6;
      } else {
        quantity = 3;
      }
      return Math.floor(Math.random() * quantity);
    },
    randomInt() {
      return Math.floor(Math.random() * 256);
    },
    createRandomStringColor() {
      var newColor =
        "rgb(" +
        this.randomInt() +
        ", " +
        this.randomInt() +
        ", " +
        this.randomInt() +
        ")";

      return newColor;
    },
    createNewColors(numbers) {
      var arr = [];
      for (var i = 0; i < numbers; i++) {
        arr.push({
          id: i,
          style: { backgroundColor: this.createRandomStringColor() },
        });
      }
      return arr;
    },
  },
};
</script>

<style>
body {
  background: #232323;
  margin: 0;
  font-family: "Montserrat", "Avenir";
}
h1 {
  font-weight: normal;
  line-height: 1.1;
  padding: 20px 0;
}
</style>
