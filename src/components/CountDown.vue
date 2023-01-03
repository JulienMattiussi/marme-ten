<template>
  <div class="main">
    <div class="countdown">
      <BeerImage :currentBeer="currentBeer" />
      <h3>Temps restant avant la fiesta :</h3>
      <table>
        <tr class="numbers">
          <td class="table-margin"></td>
          <td :class="days === 0 ? 'reached' : ''" class="days">{{ days }}</td>
          <td :class="days === 0 && hours === 0 ? 'reached' : ''">
            {{ hours }}
          </td>
          <td
            :class="days === 0 && hours === 0 && minutes === 0 ? 'reached' : ''"
          >
            {{ formatTime(minutes) }}
          </td>
          <td
            :class="
              days === 0 && hours === 0 && minutes === 0 && seconds === 0
                ? 'reached'
                : ''
            "
          >
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
          <td class="track-td" colspan="6">
            <img class="start" alt="Start" src="../assets/stan-door-crop-revert.png" />
            <VehicleImage :currentPos="currentPos" class="vehicle" />
            <img class="track" alt="Track" src="../assets/road.jpg" />
            <img class="goal" alt="Goal" src="../assets/stan-door-crop.png" />
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import VehicleImage from "./VehicleImage.vue";
import BeerImage from "./BeerImage.vue";

export default {
  name: "CountDown",
  components: {
    VehicleImage,
    BeerImage,
  },
  props: {
    startVehicle: {
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
      currentBeer: 0,
      maxPos: 100,
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
        this.currentTime > this.startVehicle
          ? 10
          : this.currentTime <= 0 || !this.currentTime
          ? this.maxPos
          : this.maxPos -
            Math.floor((this.currentTime / this.startVehicle) * this.maxPos);
      if (this.currentTime > 0) {
        setTimeout(this.countdown, this.speed);
      } else {
        this.currentTime = null;
        this.currentPos = 0;
      }
      this.currentBeer = Math.floor((this.currentPos / this.maxPos) * 9);
    },
  },
};
</script>

<style scoped>
.main {
  display: flex;
  justify-content: center;
  width: 100%;
  margin: 10px 0 0;
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

.track-td {
  position: relative;
}

img.track {
  margin-top: 50px;
  height: 50px;
  width: 100%;
}

.vehicle {
  left: 0;
  margin-top: 15px;
  width: 200px;
}

@media (max-width: 1250px) {
  img.track {
    margin-left: -10px;
    width: calc(100% + 20px);
  }
}

img.start {
  height: 130px;
  margin-top: -20px;
  margin-left: -10px;
  position: absolute;
}

img.goal {
  height: 130px;
  margin-top: -20px;
  margin-left: -80px;
  position: absolute;
}

@media (max-width: 1250px) {
  img.start {
    right: 0;
    margin-top: -110px;
    margin-left: -10px;
  }

  img.goal {
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
