<template>
  <div class="vehicle" :style="`margin-left: calc(${currentPos}% - 100px);`">
    <img alt="Vehicle" class="A" src="../assets/bikes-group-A.png" />
    <img alt="Vehicle" class="C" src="../assets/bikes-group-C.png" />
    <img alt="Vehicle" class="D" src="../assets/bikes-group-D.png" />
    <img alt="Vehicle" class="B" src="../assets/bikes-group-B.png" />
    <div class="people">
      <img class="avatar" alt="Avatar" :src="getImgUrl(avatar)" />
      <span>{{ message }}</span>
    </div>
  </div>
</template>

<script>
const avatars = [
  { image: "matthieu.jpg", message: "C'est quand qu'on arrive ?!" },
  { image: "alexandre.png", message: "On fait quoi ?" },
  { image: "anthony.png", message: "Je veux aller faire pipi !!" },
  { image: "arnaud.png", message: "Y a Julio qui m'embête." },
  { image: "florian.jpg", message: "Zzzzzzz" },
  { image: "francois.jpg", message: "Un peu de calme derrière" },
  { image: "gildas.jpg", message: "J'ai des crampes." },
  { image: "guillaume.png", message: "On sera combien ?" },
  { image: "jeremie.jpg", message: "Je revends mon sandwich." },
  { image: "jibe.png", message: "On va où ?" },
  { image: "julio.jpg", message: "Quelqu'un a de quoi manger ?" },
  { image: "karen.jpg", message: "J'ai trop trop hâte <3 !!" },
  { image: "caroline.png", message: "zu Hilfe !!" },
  { image: "guiom.png", message: "Vimenquonrive" },
  { image: "cindy.png", message: "Je vais reprendre une bière" },
  { image: "thibault.png", message: "Y aura qui ?" },
  { image: "antoine.png", message: "Vous êtes sûrs que j'ai le droit de venir ?" },
  { image: "benoit.png", message: "Vous êtes sûr qu'on va dans le bon sens ?" },
];

const getRandomInt = (max) => {
  return Math.floor(Math.random() * max);
};

export default {
  name: "VehicleImage",
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
      vehicleRotate: 3,
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
.vehicle {
  position: absolute;
  margin-top: -25px;
  height: 50px;
  width: 100px;
}

.vehicle > img {
  width: 100%;
  animation-iteration-count: infinite;
  animation-duration: 0.5s;
  animation-name: oscillatingA;
}

.vehicle > img.B {
  position: absolute;
  animation-name: oscillatingB;
  left: 0;
}

.vehicle > img.C {
  position: absolute;
  animation-name: oscillatingC;
  left: 0;
}

.vehicle > img.D {
  position: absolute;
  animation-name: oscillatingA;
  left: 0;
}

@keyframes oscillatingA {
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

@keyframes oscillatingB {
  0% {
    transform: rotate(0deg);
  }
  25% {
    transform: rotate(-3deg);
  }
  50% {
    transform: rotate(0deg);
  }
  75% {
    transform: rotate(3deg);
  }
  100% {
    transform: rotate(0deg);
  }
}

@keyframes oscillatingC {
  0% {
    transform: rotate(-3deg);
  }
  25% {
    transform: rotate(0deg);
  }
  50% {
    transform: rotate(3deg);
  }
  75% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(-3deg);
  }
}

.vehicle > .people {
  display: flex;
}

.vehicle:hover > .people {
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
  top: 75px;
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
