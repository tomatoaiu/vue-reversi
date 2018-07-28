<template>
  <main>
    <section>
      black: {{ count.black }}  white: {{ count.white }}
      <button @click="init()">init</button>
      <ul  v-for="(row, i) of board" :key="i">
        <li v-for="(column, j) of board[i]" :key="j" @click="clickedBoard(i, j)">
          <div :class="column"></div>
        </li>
      </ul>
      <p v-if="turn === 'black'">black turn</p>
      <p v-else>white turn</p>
    </section>
  </main>
</template>

<script lang="ts">
import Vue from 'vue'

const BLANK = 'blank'
const BLACK = 'black'
const WHITE = 'white'

export default Vue.extend({
  name: 'App',
  data () {
    return {
      board: [],
      turn: BLACK,
      count: {
        black: 2,
        white: 2
      }
    }
  },
  created () {
    this.init()
  },
  methods: {
    init (): void {
      this.board = []
      for (let i = 0; i < 8; i++) {
        this.board.push([])
        for (let j = 0; j < 8; j++) {
          this.board[i].push(BLANK)
        }
      }
      this.board[3][3] = BLACK
      this.board[3][4] = WHITE
      this.board[4][3] = WHITE
      this.board[4][4] = BLACK

      this.count.black = 2
      this.count.white = 2
    },
    clickedBoard (i: number, j: number): void {
      if (this.board[i][j] === BLANK) {
        if (this.turn === BLACK) {
          this.board[i][j] = BLACK
        } else {
          this.board[i][j] = WHITE
        }
        this.turn = this.turn === BLACK ? WHITE : BLACK
        this.countPiece()
      }
    },
    countPiece ():void {
      this.count.black = 0
      this.count.white = 0
      this.board.forEach((row) => {
        this.count.black += (row.filter((column) => column === BLACK)).length
        this.count.white += (row.filter((column) => column === WHITE)).length
      });
    }
  }
})
</script>

<style scoped>
main {
  width: 100vw;
  height: 100vh;
  display: table;
}

section {
  display: table-cell;
  vertical-align: middle;
  text-align: center;
}

button {
  padding: 0.2rem 0.5rem;
}

ul {
  height: 50px;
  width: 400px;
  margin: auto;
}

li {
  list-style: none;
  display: inline-block;
  width: 50px;
  height: 50px;
  background-color: green;
}

.blank, .black, .white {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}

.black {
  background-color: black;
}

.white {
  background-color: white;
}
</style>

