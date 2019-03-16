<template>
  <div class="fullCalendar">
    <div class="calendarHeader">
      <ul>
        <li @click="changeMonth(1)" style="text-align:center ">pre</li>
        <li style="text-align:center">{{year}}/{{month+1}}</li>
        <li @click="changeMonth(-1)" style="text-align:center">next</li>
      </ul>
    </div>
    <div class="calendarBody">
      <div v-for="(item) in weekday" :key="item">{{item}}</div>
      <div
        v-for="(item,index) in Dates"
        :key="index"
        :style="dateColor(item.color)"
      >{{item.date.day}}</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      weekday: ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"],
      year: "",
      month: "",
      Dates: []
    };
  },
  methods: {
    setDates(year, month) {
      const tempDay = new Date(year, month);
      this.$set(this, "year", year);
      this.$set(this, "month", month);
      this.$set(this, "Dates", []);
      const weekday = tempDay.getDay();
      tempDay.setDate(tempDay.getDate() - weekday);

      for (var i = 0; i < weekday; i++) {
        let Date = {
          date: { month: tempDay.getDate(), day: tempDay.getDate() },
          color: "rgba(53, 19, 6, 0.393)"
        };
        this.Dates.push(Date);
        tempDay.setDate(tempDay.getDate() + 1);
      }

      while (tempDay.getMonth() === month) {
        let Date = {
          date: { month: tempDay.getDate(), day: tempDay.getDate() },
          color: "rgba(53, 19, 6, 0.918)"
        };
        this.Dates.push(Date);
        tempDay.setDate(tempDay.getDate() + 1);
      }

      while (
        (this.Dates.length < 42 && this.Dates.length > 35) ||
        this.Dates.length < 35
      ) {
        let Date = {
          date: { month: tempDay.getDate(), day: tempDay.getDate() },
          color: "rgba(53, 19, 6, 0.393)"
        };
        tempDay.setDate(tempDay.getDate() + 1);
        this.Dates.push(Date);
      }
    },
    changeMonth(value) {
      let month = this.month - value;
      switch (month) {
        case -1:
          this.$set(this, "year", this.year - 1);
          this.$set(this, "month", 11);
          break;
        case 12:
          this.$set(this, "year", this.year + 1);
          this.$set(this, "month", 0);
          break;
        default:
          this.$set(this, "month", month);
          break;
      }
      this.setDates(this.year, this.month);
    },
    dateColor(color) {
      return {
        color: color
      };
    }
  },
  mounted() {
    const today = new Date();
    this.setDates(today.getFullYear(), today.getMonth());
  }
};
</script>
<style>
.fullCalendar {
  color: rgba(53, 19, 6, 0.918);
  font-size: 120%;
  max-width: 38%;
}
div.calendarHeader {
  width: 91%;
  height: 5vh;
}
.calendarHeader ul {
  list-style: none;
}
.calendarHeader li {
  position: relative;
  float: left;
  font-size: 150%;
  width: 33.3%;
  float: left;
}
.calendarBody div {
  width: 13%;
  padding: 3%;
  float: left;
  box-sizing: border-box;
}
</style>

