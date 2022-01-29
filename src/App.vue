<template>
  <form>
    <input id="date" v-model="dateString" type="date" />
    <label for="date"></label>
    <input id="date" v-model="timeString" type="time" />
    <label for="time"></label>
    {{ zoneString }}
    <TimeZonesList :startingZone="zoneString" />
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
        console.log(newDate);
        const change = DateTime.fromISO(newDate);
        this.datetime = this.datetime.set({
          hour: change.hour,
          minute: change.minute,
        });
      },
    },
    zoneString: {
      get: function (): string {
        return this.datetime.zoneName;
      },
      set: function (newZone: string): void {
        this.datetime = this.datetime.setZone(newZone);
      },
    },
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
