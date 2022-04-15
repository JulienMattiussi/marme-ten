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
import lorrainjs from "lorrainjs";

console.log("lorrainjs");

const testA = "Michel est parti";
const testB = "Jacky est revenu";

lorrainjs.originalLog("Sans changement :");
console.log(testA);
lorrainjs.originalLog("Traduction manuelle de chaine :");
console.log(lorrainjs.translate(testA));

lorrainjs.initLog();
lorrainjs.initWarn({ le: true });
lorrainjs.initError({ gros: true });

lorrainjs.originalLog("Traduction automatique :");
console.log(testA);
lorrainjs.originalWarn("Traduction automatique en warning :");
console.warn(testB);
lorrainjs.originalError("Traduction automatique en error :");
console.error(testB);

lorrainjs.originalLog("Avec object :");
console.log({ testA, testB });

lorrainjs.originalLog("Avec array :");
console.log([testA, testB]);

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
