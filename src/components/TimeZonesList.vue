<template>
  <select
    v-model="selectedZone"
    @change="$emit('changed', $event.target.value)"
  >
    <option v-for="(zone, index) in zones" :key="index">
      {{ zone }}
    </option>
  </select>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import * as moment from "moment-timezone";

export default defineComponent({
  name: "CopyBox",
  props: {
    startingZone: String,
  },
  emits: ["changed"],
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
