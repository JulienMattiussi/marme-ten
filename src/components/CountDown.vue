<template>
  <div class="main">
    <div class="countdown">
      <h3>Temps restant avant la fiesta :</h3>
      <table>
        <tr class="numbers">
          <td class="table-margin"></td>
          <td :class="days === 0 ? 'reached' : ''" class="days">{{ days }}</td>
          <td :class="hours === 0 ? 'reached' : ''">{{ hours }}</td>
          <td :class="minutes === 0 ? 'reached' : ''">
            {{ formatTime(minutes) }}
          </td>
          <td :class="seconds === 0 ? 'reached' : ''">
            {{ formatTime(seconds) }}
          </td>
          <td class="table-margin"></td>
        </tr>
        <tr class="labels">
          <td class="table-margin"></td>
          <td>jour{{ days > 1 ? "s" : "" }}</td>
          <td>heure{{ hours > 1 ? "s" : "" }}</td>
          <td>minute{{ minutes > 1 ? "s" : "" }}</td>
          <td>seconde{{ seconds > 1 ? "s" : "" }}</td>
          <td class="table-margin"></td>
        </tr>
        <tr>
          <td colspan="6">
            <BusImage :currentPos="currentPos" />
            <img class="road" alt="Road" src="../assets/road.jpg" />
            <img class="mountain" alt="Mountain" src="../assets/mountain.png" />
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import BusImage from "./BusImage.vue";

export default {
  name: "CountDown",
  components: {
    BusImage,
  },
  props: {
    startbus: {
      type: Number,
      default: 2600000000,
    },
    deadline: {
      type: String,
      required: true,
    },
    speed: {
      type: Number,
      default: 1000,
    },
  },
  data: function () {
    return {
      currentTime: null,
      currentPos: 0,
      maxPos: 600,
    };
  },
  mounted() {
    setTimeout(this.countdown, 1);
  },
  computed: {
    seconds() {
      return Math.floor((this.currentTime / 1000) % 60);
    },
    minutes() {
      return Math.floor((this.currentTime / 1000 / 60) % 60);
    },
    hours() {
      return Math.floor((this.currentTime / (1000 * 60 * 60)) % 24);
    },
    days() {
      return Math.floor(this.currentTime / (1000 * 60 * 60 * 24));
    },
  },
  methods: {
    formatTime(value) {
      if (value < 10) {
        return "0" + value;
      }
      return value;
    },
    countdown() {
      this.currentTime = Date.parse(this.deadline) - Date.parse(new Date());
      this.currentPos =
        this.currentTime > this.startbus
          ? 0
          : this.currentTime <= 0 || !this.currentTime
          ? this.maxPos
          : this.maxPos -
            Math.floor((this.currentTime / this.startbus) * this.maxPos);
      if (this.currentTime > 0) {
        setTimeout(this.countdown, this.speed);
      } else {
        this.currentTime = null;
        this.currentPos = 0;
      }
    },
  },
};
</script>

<style scoped>
.main {
  display: flex;
  justify-content: center;
  width: 100%;
  margin: 40px 0 0;
}

.countdown {
  display: flex;
  flex-direction: column;
  width: 700px;
}

.numbers {
  font-size: 60px;
  color: red;
  vertical-align: bottom;
}

.reached {
  color: green !important;
}

@media (max-width: 1250px) {
  .numbers {
    font-size: 45px;
  }
}

.labels {
  font-size: 20px;
}

.days {
  font-size: 100px;
  color: brown;
  vertical-align: bottom;
  line-height: 100px;
}

img.road {
  margin-top: 50px;
  height: 50px;
  width: 100%;
}

@media (max-width: 1250px) {
  img.road {
    margin-left: -10px;
    width: calc(100% + 20px);
  }
}

img.mountain {
  height: 130px;
  margin-top: -5px;
  margin-left: -80px;
  position: absolute;
}

@media (max-width: 1250px) {
  img.mountain {
    right: 0;
    margin-top: -110px;
    margin-left: unset;
    margin-right: -50px;
  }
}

.table-margin {
  width: 100px;
}

@media (max-width: 1250px) {
  .table-margin {
    width: 0px;
  }
}
</style>
