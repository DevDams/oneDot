<template>
  <div id="app">
    <Game :player="player" @score="updateScore"/>
    <Player v-on:player="updatePlayer"/>
    <Score :score="score" :player="player"/>
  </div>
</template>

<script>
import Game from './components/Game'
import Score from './components/Score'
import Player from './components/Player'

export default {
  name: 'App',
  data: function () {
    return {
      score: 0,
      player: false
    }
  },
  components: {
    Game,
    Score,
    Player
  },
  methods: {
    updateScore: function (score) {
      this.score = score
    },
    updatePlayer: function () {
      this.player = true
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Grandstander:ital,wght@0,500;1,400&display=swap');

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 80%;
  height: 500px;
  display: block;
  margin: auto;
  background: #9c89b8;
}
</style>
