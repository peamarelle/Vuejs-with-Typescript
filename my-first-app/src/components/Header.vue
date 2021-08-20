<template>
    <p class="h1">{{ msg }}</p>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default {
  name: 'Header',
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  font-family: 'Courier New', Courier, monospace;
  text-align: left;
}
</style>
