<template>
  <div @click="copy">
    <span class="material-icons material-icons-outlined icon"
      >content_copy</span
    >
    <span>{{ text }}</span>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "CopyBox",
  props: {
    text: {
      type: String,
      required: true,
    },
  },
  methods: {
    copy(): void {
      navigator.clipboard.writeText(this.text);
    },
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div {
  padding: 5px 15px;
  border: 1px solid #d3d7db;
  border-radius: 15px;
  vertical-align: middle;
  background: linear-gradient(90deg, #0eb5c4 24%, #fafafc 24%);
  cursor: pointer;
  box-shadow: 2px 2px 2px #bfbcbc;
}

div:hover {
  box-shadow: 2px 3px 3px #aaa;
}

div:active {
  box-shadow: 0px 0px 0px #aaa;
}

span {
  vertical-align: middle;
}

span.icon {
  margin-right: 20px;
}
</style>
