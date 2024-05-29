<template>
  <div class="game">
    <Board :squares="squares" @square-click="handleSquareClick" />
    <p>{{ status }}</p>
    <button @click="resetGame">Reset Game</button>
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import Board from './Board.vue';

export default {
  components: { Board },
  setup() {
    const squares = ref(Array(9).fill(null));
    const xIsNext = ref(true);

    const status = computed(() => {
      const winner = calculateWinner(squares.value);
      return winner
          ? `Winner: ${winner}`
          : `Next player: ${xIsNext.value ? 'X' : 'O'}`;
    });

    function handleSquareClick(index) {
      if (squares.value[index] || calculateWinner(squares.value)) return;
      squares.value.splice(index, 1, xIsNext.value ? 'X' : 'O');
      xIsNext.value = !xIsNext.value;
    }

    function resetGame() {
      squares.value = Array(9).fill(null);
      xIsNext.value = true;
    }

    return { squares, handleSquareClick, status, resetGame };
  }
};

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}
</script>

<style scoped>
.game {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
