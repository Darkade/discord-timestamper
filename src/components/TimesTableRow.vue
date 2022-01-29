<template>
  <tr>
    <td>{{ secondsString }}</td>
    <td>{{ formatString }}</td>
  </tr>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { DateTime } from "luxon";

export default defineComponent({
  name: "CopyBox",
  props: {
    datetime: {
      type: DateTime,
      required: true,
    },
    format: String,
  },
  computed: {
    secondsString(): string {
      const seconds: number = this.datetime.toSeconds() | 0;
      return `<t:${seconds}:${this.format}>`;
    },
    formatString(): string {
      switch (this.format) {
        case "d": // <t:1643481240:d> 01/29/2022
          return this.datetime.toFormat("D");
        case "D": // <t:1643481240:D>  January 29, 2022
          return this.datetime.toFormat("DDD");
        case "t": // <t:1643481240:t>  12:34 PM
          return this.datetime.toFormat("t");
        case "T": // <t:1643481240:T>  12:34:00 PM
          return this.datetime.toFormat("tt");
        case "f": // <t:1643481240:f>  January 29, 2022 12:34 PM
          return this.datetime.toFormat("ff");
        case "F": // <t:1643481240:F>  Saturday, January 29, 2022 12:34 PM
          return this.datetime.toFormat("ffff");
        case "R": // <t:1643481240:R>  an hour ago
          return this.datetime.toRelative() ?? "";
        default:
          return "";
      }
    },
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
