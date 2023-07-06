<template>
  <div class="game">
    <h1 class="title">Rock Paper Scissors</h1>
    <div class="buttons">
      <button @click="makeMove('rock')">Rock</button>
      <button @click="makeMove('paper')">Paper</button>
      <button @click="makeMove('scissors')">Scissors</button>
    </div>
    <div v-if="result" class="result">
      <p>You chose: {{ playerMove }}</p>
      <p>Computer chose: {{ computerMove }}</p>
      <p>{{ result }}</p>
    </div>
    <button @click="resetGame">Reset Game</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      playerMove: '',
      computerMove: '',
      result: '',
    };
  },
  methods: {
    makeMove(move) {
      this.playerMove = move;
      this.computerMove = this.getRandomMove();

      if (this.playerMove === this.computerMove) {
        this.result = "It's a tie!";
      } else if (
        (this.playerMove === 'rock' && this.computerMove === 'scissors') ||
        (this.playerMove === 'paper' && this.computerMove === 'rock') ||
        (this.playerMove === 'scissors' && this.computerMove === 'paper')
      ) {
        this.result = 'You win!';
      } else {
        this.result = 'You lose!';
      }
    },
    getRandomMove() {
      const moves = ['rock', 'paper', 'scissors'];
      const randomIndex = Math.floor(Math.random() * moves.length);
      return moves[randomIndex];
    },
    resetGame() {
      this.playerMove = '';
      this.computerMove = '';
      this.result = '';
    },
  },
};
</script>

<style scoped>
.game {
  text-align: center;
  margin-top: 60px;
  border: 6px solid rgb(61, 103, 60);
}

.title {
  color: rgb(61, 103, 60);
}

.buttons {
  margin: 20px;
}

.result {
  margin-top: 20px;
}
</style>
