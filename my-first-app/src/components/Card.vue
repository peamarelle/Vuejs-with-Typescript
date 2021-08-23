<template>
<div class="alert" :class="[ isEditing ? warning : primary ]">
  <div class="d-flex justify-content-between">
    <div>
      {{ title }}
    </div>
    <div>
      <button class="btn btn-success btn-sm"
       @click="edit"><i class="fas fa-edit"></i></button>
      <button class="btn btn-danger btn-sm"><i class="fas fa-trash-alt"></i></button>
    </div>
  </div>
</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Card',
  props: {
    title: String,
  },
  data() {
    return {
      isEditing: false,
      primary: 'alert-primary',
      warning: 'alert-warning',
    };
  },
  methods: {
    edit():void {
      this.isEditing = true;
      this.$emit('message', this.title);
    },
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
a {
  color: #42b983;
}
</style>
