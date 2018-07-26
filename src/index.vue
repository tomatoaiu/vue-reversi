<template>
  <main>
    <section>
      <button @click="init()">init</button>
      <ul  v-for="(row, i) of board" :key="i">
        <li v-for="(column, j) of board[i]" :key="j" @click="clickedBoard($event, i, j)">
          <div v-if="column === 0" class="blank"></div>
          <div v-else-if="column === 1" class="black"></div>
          <div v-else-if="column === 2" class="white"></div>
        </li>
      </ul>
      <p v-if="turn === 1">black turn</p>
      <p v-else>white turn</p>
    </section>
  </main>
</template>

<script lang="ts">
import Vue from 'vue'

const BLANK = 0
const BLACK = 1
const WHITE = 2

export default Vue.extend({
  name: 'App',
  data () {
    return {
      board: [],
      turn: 1 // 1: black, 2: white
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
    },
    clickedBoard (event: Event, i: number, j: number): void {
      if (this.board[i][j] === BLANK) {
        (<HTMLElement>event.target).classList.remove('blank')
        if (this.turn === BLACK) {
          (<HTMLElement>event.target).classList.add('black')
        } else {
          (<HTMLElement>event.target).classList.add('white')
        }
        this.board[i][j] = this.turn
        this.turn = this.turn === BLACK ? WHITE : BLACK
      }
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

