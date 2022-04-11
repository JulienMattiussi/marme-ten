<template>
  <div class="bus" :style="`margin-left: ${currentPos}px;`">
    <img
      :style="`transform: rotate(${busRotate}deg);`"
      alt="Bus"
      src="../assets/bus.png"
    />
    <div class="people">
      <img
        class="avatar"
        :style="`transform: rotate(${busRotate}deg);`"
        alt="Avatar"
        :src="getImgUrl(avatar)"
      /><span>C'est quand qu'on arrive ?!</span>
    </div>
  </div>
</template>

<script>
const avatars = [
  "matthieu.jpg",
  "alexandre.png",
  "anthony.png",
  "arnaud.png",
  "florian.jpg",
  "francois.jpg",
  "gildas.jpg",
  "guillaume.png",
  "jeremie.jpg",
  "jibe.png",
  "julio.jpg",
  "karen.jpg",
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
    maxPos: {
      type: Number,
      required: true,
    },
    moveSpeed: {
      type: Number,
      default: 300,
    },

    changeSpeed: {
      type: Number,
      default: 3000,
    },
  },
  data: function () {
    return {
      busRotate: 3,
      avatar: "matthieu.jpg",
    };
  },
  mounted() {
    setTimeout(this.moving, 1);
    setTimeout(this.changing, 1);
  },
  methods: {
    getImgUrl(img) {
      var getImage = require.context("../assets/avatars", false, /\.*$/);
      return getImage("./" + img);
    },
    moving() {
      this.busRotate = this.busRotate != 3 ? 3 : -3;
      if (this.currentPos < this.maxPos) {
        setTimeout(this.moving, this.moveSpeed);
      }
    },
    changing() {
      const choice = getRandomInt(avatars.length);
      this.avatar = avatars[choice];
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
}
</style>
