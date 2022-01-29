<template>
  <form>
    <input id="date" v-model="datetime" type="datetime" />
    <label for="date"></label>
    <input id="date" v-model="time" type="datetime" />
    <label for="time"></label>
    <input id="timezone" v-model="timezone" type="datetime" />
    <label for="timezone"></label>
  </form>
  <table>
    <thead>
      <td>If you paste this in chat</td>
      <td>you will get</td>
    </thead>
    <tbody>
        <CopyBox :datetime="datetime" format="d" />
        <CopyBox :datetime="datetime" format="D" />
        <CopyBox :datetime="datetime" format="t" />
        <CopyBox :datetime="datetime" format="T" />
        <CopyBox :datetime="datetime" format="f" />
        <CopyBox :datetime="datetime" format="F" />
        <CopyBox :datetime="datetime" format="R" />
    </tbody>
  </table>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { DateTime } from "luxon";
import CopyBox from "./components/CopyBox.vue";

export default defineComponent({
  name: "App",
  components: {
    CopyBox,
  },
  data() {
    return {
      datetime: DateTime.now(),
      time: 123,
      timezone: "America/Mexico_City",
    };
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
