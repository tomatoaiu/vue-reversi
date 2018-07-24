<template>
  <div>
    <ul  v-for="(row, i) of board" :key="i">
      <li v-for="(column, j) of board[i]" :key="j">
        <div v-if="column === 0" class="blank"></div>
        <div v-else-if="column === 1" class="black"></div>
        <div v-else-if="column === 2" class="white"></div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'App',
  data () {
    return {
      board: []
    }
  },
  created () {
    for (let i = 0; i < 8; i++) {
      this.board.push([])
      for (let j = 0; j < 8; j++) {
        this.board[i].push(0)
      }
    }
    this.board[3][3] = 1
    this.board[3][4] = 2
    this.board[4][3] = 2
    this.board[4][4] = 1
  }
})
</script>

<style scoped>
ul {
  height: 20px;
  width: 160px;
}

li {
  list-style: none;
  display: inline-block;
  width: 20px;
  height: 20px;
  background-color: green;
}

.blank, .black, .white {
  width: 20px;
  height: 20px;
  border-radius: 10px;
}

.black {
  background-color: black;
}

.white {
  background-color: white;
}
</style>

