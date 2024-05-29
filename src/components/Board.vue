<template>
  <div class="board">
    <Square
        v-for="(value, index) in squares"
        :key="index"
        :value="value"
        @click="() => handleClick(index)"
    />
  </div>
</template>

<script>
import Square from './Square.vue';

export default {
  components: { Square },
  props: ['squares'],
  methods: {
    handleClick(index) {
      this.$emit('square-click', index);
    }
  }
};
</script>

<style scoped>
.board {
  display: grid;
  grid-template-columns: repeat(3, 100px);
  grid-template-rows: repeat(3, 100px);
}
</style>
