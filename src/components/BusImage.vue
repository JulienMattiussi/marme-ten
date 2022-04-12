<template>
  <div class="bus" :style="`margin-left: ${currentPos}px;`">
    <img alt="Bus" src="../assets/bus.png" />
    <div class="people">
      <img class="avatar" alt="Avatar" :src="getImgUrl(avatar)" />
      <span>{{ message }}</span>
    </div>
  </div>
</template>

<script>
const avatars = [
  { image: "matthieu.jpg", message: "C'est quand qu'on arrive ?!" },
  { image: "alexandre.png", message: "Je suis malade en voiture ;(" },
  { image: "anthony.png", message: "Je veux aller faire pipi !!" },
  { image: "arnaud.png", message: "Y a Matthieu qui m'embête." },
  { image: "florian.jpg", message: "Zzzzzzz" },
  { image: "francois.jpg", message: "Un peu de calme derrière" },
  { image: "gildas.jpg", message: "J'ai des crampes." },
  { image: "guillaume.png", message: "C'est trop long." },
  { image: "jeremie.jpg", message: "Je revends mon sandwich." },
  { image: "jibe.png", message: "On va ou ?" },
  { image: "julio.jpg", message: "Quelqu'un à de quoi manger ?" },
  { image: "karen.jpg", message: "J'ai trop trop hâte <3 !!" },
  { image: "caroline.png", message: "zu Hilfe !!" },
];

const getRandomInt = (max) => {
  return Math.floor(Math.random() * max);
};

export default {
  name: "BusImage",
  props: {
    currentPos: {
      type: Number,
      required: true,
    },
    changeSpeed: {
      type: Number,
      default: 3000,
    },
  },
  data: function () {
    return {
      busRotate: 3,
      avatar: avatars[0].image,
      message: avatars[0].message,
    };
  },
  mounted() {
    setTimeout(this.changing, 1);
  },
  methods: {
    getImgUrl(img) {
      var getImage = require.context("../assets/avatars", false, /\.*$/);
      return getImage("./" + img);
    },
    changing() {
      const choice = getRandomInt(avatars.length);
      this.avatar = avatars[choice].image;
      this.message = avatars[choice].message;
      setTimeout(this.changing, this.changeSpeed);
    },
  },
};
</script>

<style scoped>
.bus {
  position: absolute;
  margin-top: 50px;
  height: 50px;
  width: 100px;
}

.bus > img {
  width: 100%;
  animation-iteration-count: infinite;
  animation-duration: 0.5s;
  animation-name: oscillating;
}

@keyframes oscillating {
  0% {
    transform: rotate(3deg);
  }
  25% {
    transform: rotate(0deg);
  }
  50% {
    transform: rotate(-3deg);
  }
  75% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(3deg);
  }
}

.bus > .people {
  display: flex;
}

.bus:hover > .people {
  display: flex;
}

.people {
  background-color: white;
  border-radius: 20px;
  padding: 10px;
  font-weight: bold;
  width: 240px;
  margin-left: -50px;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.people > span {
  min-width: 55%;
}

.people::before {
  content: "\A";
  border-style: solid;
  border-width: 0px 10px 15px 10px;
  border-color: transparent transparent white transparent;
  position: absolute;
  left: 45px;
  top: 45px;
}

.avatar {
  width: 50%;
  margin-bottom: -30px;
  border-radius: 50px;
  clip-path: polygon(100% 0%, 100% 70%, 0% 70%, 0% 0%);
  animation-iteration-count: infinite;
  animation-duration: 0.5s;
  animation-name: oscillating;
}
</style>
