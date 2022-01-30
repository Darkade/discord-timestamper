<template>
  <form>
    <input id="date" v-model="dateString" type="date" />
    <label for="date"></label>
    <input id="date" v-model="timeString" type="time" />
    <label for="time"></label>
    <TimeZonesList :startingZone="zoneString" @changed="test" />
  </form>
  <table>
    <thead>
      <td>If you paste this in chat</td>
      <td>you will get</td>
    </thead>
    <tbody>
      <TimesTableRow :datetime="datetime" format="d" />
      <TimesTableRow :datetime="datetime" format="D" />
      <TimesTableRow :datetime="datetime" format="t" />
      <TimesTableRow :datetime="datetime" format="T" />
      <TimesTableRow :datetime="datetime" format="f" />
      <TimesTableRow :datetime="datetime" format="F" />
      <TimesTableRow :datetime="datetime" format="R" />
    </tbody>
  </table>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { DateTime } from "luxon";
import TimesTableRow from "./components/TimesTableRow.vue";
import TimeZonesList from "./components/TimeZonesList.vue";

export default defineComponent({
  name: "App",
  components: {
    TimesTableRow,
    TimeZonesList,
  },
  data() {
    return {
      datetime: DateTime.now(),
    };
  },
  computed: {
    dateString: {
      get: function (): string {
        return this.datetime.toFormat("yyyy-LL-dd");
      },
      set: function (newDate: string): void {
        const change = DateTime.fromISO(newDate);
        this.datetime = this.datetime.set({
          year: change.year,
          month: change.month,
          day: change.day,
        });
      },
    },
    timeString: {
      get: function (): string {
        return this.datetime.toFormat("HH:mm");
      },
      set: function (newDate: string): void {
        const change = DateTime.fromISO(newDate);
        this.datetime = this.datetime.set({
          hour: change.hour,
          minute: change.minute,
        });
      },
    },
    zoneString(): string {
      return this.datetime.zoneName;
    },
  },
  methods: {
    test(newZone: string) {
      this.datetime = this.datetime.setZone(newZone);
    },
  },
});
</script>

<style>
body {
  margin: 0;
  min-height: 100%;
  background-color: #fff;
  font-family: "Plus Jakarta Display", sans-serif;
  color: #62668a;
  font-size: 16px;
  line-height: 1.688em;
  background-color: #fafafc;
  letter-spacing: -0.01em;
}

* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

form {
  max-width: 790px;
  margin-right: auto;
  margin-left: auto;
  padding: 32px;
}

table {
  max-width: 790px;
  margin-right: auto;
  margin-left: auto;
  padding: 32px;
  border: 0.5px solid #e7e8f1;
  border-radius: 36px;
  background-color: #fff;
  box-shadow: 0 0 6px 0 rgb(78 42 222 / 2%), 0 6px 18px 0 rgb(78 42 222 / 2%);
  transform: translate3d(0px, 0px, 0px) scale3d(1, 1, 1) rotateX(0deg)
    rotateY(0deg) rotateZ(0deg) skew(0deg, 0deg);
  opacity: 1;
  transform-style: preserve-3d;
  -webkit-transition: box-shadow 350ms, border-color 350ms,
    -webkit-transform 350ms;
  transition: box-shadow 350ms, border-color 350ms, transform 350ms,
    -webkit-transform 350ms;
  font-size: 18px;
  line-height: 35px;
  border-spacing: 0.5rem;
}

table:hover {
  border-color: #7dc9d6;
  box-shadow: 0 0 15px 0 rgb(78 42 222 / 2%), 0 15px 20px 0 rgb(78 42 222 / 2%);
  -ms-transform: translate(0, -5px);
}

input {
  padding: 10px;
  height: 40px;
  margin: 10px 7px;
  font-size: 18px;
  line-height: 26px;
  border-radius: 10px;
  background-color: #0eb5c4;
  color: white;
  border: none;
  font-weight: 600;
  text-align: center;
  box-shadow: 0 2px 6px 0 rgb(72 117 125 / 16%);
}

input:hover {
  box-shadow: 0 8px 20px 0 rgb(125 201 214 / 30%);
  -webkit-transform: translate(0, -2px);
  -ms-transform: translate(0, -2px);
  transform: translate(0, -2px);
  color: #fff;
  -webkit-transition: box-shadow 350ms, -webkit-transform 350ms;
  transition: transform 350ms, box-shadow 350ms, -webkit-transform 350ms;
}

html {
  font-family: sans-serif;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  height: 100%;
}

table thead td {
  font-weight: bold;
}
</style>
