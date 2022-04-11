<template>
  <div class="main">
    <div class="countdown">
      <h3>Temps restant avant la fiesta :</h3>
      <table>
        <tr class="numbers">
          <td class="table-margin"></td>
          <td class="days">{{ days }}</td>
          <td>{{ hours }}</td>
          <td>{{ formatTime(minutes) }}</td>
          <td>{{ formatTime(seconds) }}</td>
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
            <img class="bus" alt="Bus" src="../assets/bus.png" />
            <img class="road" alt="Road" src="../assets/road.jpg" />
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "CountDown",
  props: {
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
      if (this.currentTime > 0) {
        setTimeout(this.countdown, this.speed);
      } else {
        this.currentTime = null;
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
img.bus {
  position: absolute;
  margin-top: 50px;
  height: 50px;
}
.table-margin {
  width: 100px;
}
</style>
