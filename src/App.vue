<template>
  <img class="back" alt="Ocean" src="./assets/back-light.jpg" />
  <div class="content">
    <img alt="Marmelab logo" src="./assets/logo-green.png" />
    <TitleMessage msg="En janvier, c'est LES 10 ANS !!!" />
    <CountDown deadline="2023-01-19T19:00:00.000Z" />
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

@media (max-width: 1250px) {
  #app {
    padding-top: 10px;
  }
}

.back {
  width: calc(100% - 60px);
  margin: 30px;
  position: absolute;
  top: 0;
  left: 0;
  filter: contrast(40%) blur(5px) brightness(1.5);
}

@media (max-width: 1250px) {
  .back {
    margin: -10px;
    height: calc(100% + 20px);
    width: unset;
  }
}

.content {
  position: relative;
}
</style>
