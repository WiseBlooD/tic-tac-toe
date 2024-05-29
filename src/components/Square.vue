<template>
  <button class="square" @click="$emit('click')">
    {{ value }}
  </button>
</template>

<script>
export default {
  props: ['value']
};
</script>

<style scoped>
.square {
  width: 100px;
  height: 100px;
  font-size: 24px;
}
</style>
