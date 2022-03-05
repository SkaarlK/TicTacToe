<template>
  <div>
    <h1>TicTacToe</h1>
    <v-container id="board">
      <div v-for="(n, i) in 3" :key="i">
        <div v-for="(n, j) in 3" :key="j">
          <Cell @clicked="mark(i,j)" :check="board[i][j]"/>
        </div>
      </div>
    </v-container>
    <h1 style="color: green;">Winner:
      <span v-show="winner">
      </span>
        {{winner || this.game >= 9 ? this.player : ''}}
    </h1>
    <v-btn dark @click="reset">RESET</v-btn>
  </div>
</template>

<script>
import Cell from './Cell.vue';

export default {
  name: 'Board',
  components: {
    Cell,
  },
  data: () => ({
    board: [
      ['', '', ''],
      ['', '', ''],
      ['', '', ''],
    ],
    player: 'O',
    game: 0,
  }),
  computed: {
    winner() {
      return this.checkRows();
    },
  },
  methods: {
    mark(i, j) {
      if (!this.checkRows()) {
        if (this.board[i][j] !== '') {
          return false;
        }
        this.player = this.player === 'X' ? 'O' : 'X';
        this.board[i][j] = this.player;
        this.game += 1;
        this.$forceUpdate();
        return true;
      }
      return undefined;
    },
    checkRows() {
      for (let i = 0; i < 3; i += 1) {
        if (
          this.board[0][i] === this.player
          && this.board[1][i] === this.player
          && this.board[2][i] === this.player
        ) {
          console.log('Venceu horizontalmente.');
          return true;
        }
      }
      for (let i = 0; i < 3; i += 1) {
        if (
          this.board[i][0] === this.player
          && this.board[i][1] === this.player
          && this.board[i][2] === this.player
        ) {
          console.log('Venceu verticalmente.');
          return true;
        }
      }
      if (
        this.board[0][0] === this.player
      && this.board[1][1] === this.player
      && this.board[2][2] === this.player
      ) {
        console.log('Venceu diagonalmente.');
        return true;
      }
      if (
        this.board[1][0] === this.player
        && this.board[1][1] === this.player
        && this.board[0][2] === this.player
      ) {
        return true;
      }
      if (this.game > 8) this.player = 'DRAW';
      return false;
    },
    reset() {
      this.board = [
        ['', '', ''],
        ['', '', ''],
        ['', '', ''],
      ];
      this.game = 0;
      this.player = 'O';
    },
  },
};
</script>

<style scoped>
#board {
    display: flex;
    flex-wrap: wrap;
    padding: 0;
    width: 350px;
    height: 350px;
    border: 1px solid black;
  }
</style>
