<script setup>
import SquareComponent from './SquareComponent.vue'
import {onUpdated, reactive} from "vue";

const board = reactive({
  squares: Array(9).fill(null),
  isNextX: true,
  winner: null,
  status: 'Next player: X',
});

onUpdated(() => {
  if (board.winner) {
    board.status = `Winner: ${board.winner}`;
  } else if (board.squares.includes(null)) {
    board.status = `Next player: ${board.isNextX ? 'X' : 'O'}`;
  } else {
    board.status = 'Draw';
  }
})

const handleClick = (i) => {
  if (calculateWinner() || board.squares[i]) {
    return;
  }

  board.squares[i] = board.isNextX ? 'X' : 'O';
  board.isNextX = !board.isNextX;
  board.status = `Next player: ${board.isNextX ? 'X' : 'O'}`;
  board.winner = calculateWinner(board.squares);
}

const calculateWinner = () => {
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
    if (board.squares[a] && board.squares[a] === board.squares[b] && board.squares[a] === board.squares[c]) {
      return board.squares[a];
    }
  }
  return null;
}


</script>

<template>
  <div>
    <div class="status">{{ board.status }}</div>
    <div class="board-row">
      <SquareComponent :value="board.squares[0]" @on-click="handleClick(0)"/>
      <SquareComponent :value="board.squares[1]" @on-click="handleClick(1)"/>
      <SquareComponent :value="board.squares[2]" @on-click="handleClick(2)"/>
    </div>
    <div class="board-row">
      <SquareComponent :value="board.squares[3]" @on-click="handleClick(3)"/>
      <SquareComponent :value="board.squares[4]" @on-click="handleClick(4)"/>
      <SquareComponent :value="board.squares[5]" @on-click="handleClick(5)"/>
    </div>
    <div class="board-row">
      <SquareComponent :value="board.squares[6]" @on-click="handleClick(6)"/>
      <SquareComponent :value="board.squares[7]" @on-click="handleClick(7)"/>
      <SquareComponent :value="board.squares[8]" @on-click="handleClick(8)"/>
    </div>
  </div>
</template>

<style scoped>

</style>
