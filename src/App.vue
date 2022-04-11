<template>
  <img class="back" alt="Vosges" src="./assets/back-light.jpeg" />
  <div class="content">
    <img alt="Marmelab logo" src="./assets/logo-green.png" />
    <TitleMessage msg="En mai, on fait ce qui nous plait !" />
    <CountDown deadline="2022-05-10T15:30:00.000Z" />
  </div>
</template>

<script>
import TitleMessage from "./components/TitleMessage.vue";
import CountDown from "./components/CountDown.vue";

export default {
  name: "App",
  components: {
    TitleMessage,
    CountDown,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
}
.back {
  width: calc(100% - 60px);
  margin: 30px;
  position: absolute;
  top: 0;
  left: 0;
  filter: contrast(40%) blur(5px) brightness(1.5);
}
.content {
  position: relative;
}
</style>
