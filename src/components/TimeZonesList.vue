<template>
  <select v-model="selectedZone">
    <option v-for="(zone, index) in zones" :key="index">
      {{ zone }}
    </option>
  </select>
  <span>Selected: {{ selectedZone }}</span>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import * as moment from "moment-timezone";

export default defineComponent({
  name: "CopyBox",
  props: {
    startingZone: String,
  },
  data() {
    return {
      zones: moment.tz.names(),
      selectedZone: this.startingZone,
    };
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
