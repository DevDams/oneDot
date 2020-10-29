<template>
    <div class="info">
        <span v-html="welcomeMessage" :class="{ hide : !player }" class="welcomeMessage">{{ welcomeMessage }}</span>
        <form v-on:submit.prevent="setPlayer" :class="{ hide : player }">
            <input type="text" name="player" placeholder="Entrez votre nom de joueur">
            <button type="submit">Jouer</button>
        </form>
    </div>
</template>

<script>
export default {
  name: 'Player',
  data: function () {
    return {
      player: '',
      welcomeMessage: ''
    }
  },
  updated: function () {
    this.welcomeMessage = `Bonjour <span class="player">${this.player}</span> !`
  },
  methods: {
    setPlayer: function (event) {
      let playerName = event.target[0].value

      if (!playerName) {
        window.alert('Veillez reseigner votre nom svp !')
        return
      }

      this.player = playerName
      this.$emit('player')
    }
  }
}
</script>

<style scoped>
    .hide {
        display: none;
    }

    .info {
      margin-top: 40px;
      text-align: center;
    }

    .welcomeMessage {
      font-weight: 700;
    }

    input[type="text"] {
      border: 1px solid #334455;
      border-radius: 5px;
      padding: 7px 20px;
    }

    button[type="submit"] {
      background: #b8bedd;
      color: #f0e6ef;
      font-weight: 700;
      border: none;
      border-radius: 5px;
      padding: 7px 20px;
      cursor: pointer;
    }
</style>
