<template>
  <div class="main">
    <div class="countdown">
      <h3>Temps restant avant la fiesta :</h3>
      <table>
        <tr class="numbers">
          <td class="days">{{ days }}</td>
          <td>{{ hours }}</td>
          <td>{{ formatTime(minutes) }}</td>
          <td>{{ formatTime(seconds) }}</td>
        </tr>
        <tr class="labels">
          <td>jour{{ days > 1 ? "s" : "" }}</td>
          <td>heure{{ hours > 1 ? "s" : "" }}</td>
          <td>minute{{ minutes > 1 ? "s" : "" }}</td>
          <td>seconde{{ seconds > 1 ? "s" : "" }}</td>
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
  width: 500px;
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
</style>
