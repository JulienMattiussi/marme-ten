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

function showGros(arg) {
  const gros = " gros";
  if (typeof arg === "object") {
    const newObject = Object.assign({}, arg);
    Object.keys(newObject).forEach((key) => {
      newObject[key] = newObject[key] + gros;
    });
    return newObject;
  }
  return arg + gros;
}

const regexCapital = /\b[A-Z][a-zA-Z]*\b/;

function showLe(arg) {
  const le = "le ";
  if (typeof arg === "object") {
    const newObject = Object.assign({}, arg);
    Object.keys(newObject).forEach((key) => {
      if (typeof newObject[key] === "string") {
        newObject[key] = newObject[key].replace(regexCapital, `${le}$&`);
      }
    });
    return newObject;
  }
  return arg.replace(regexCapital, `${le}$&`);
}

var orig = console.log;

console.log = function () {
  var msgs = [];

  while (arguments.length) {
    const argument = [].shift.call(arguments);
    msgs.push(showLe(showGros(argument)));
  }

  orig.apply(console, msgs);
};

//console.log("TUTU");
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
