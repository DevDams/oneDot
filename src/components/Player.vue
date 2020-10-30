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
      margin-top: 10px;
      text-align: center;
      font-family: 'Grandstander', cursive;
      letter-spacing: 2px;
    }

    .welcomeMessage {
      font-weight: 700;
      font-family: 'Grandstander', cursive;
      letter-spacing: 2px;
    }

    input[type="text"] {
      border: 2px solid #334455;
      border-radius: 5px;
      padding: 15px 30px;
      font-family: 'Grandstander', cursive;
      letter-spacing: 2px;
    }

    button[type="submit"] {
      background: #b8bedd;
      color: #000;
      font-weight: 600;
      font-family: 'Grandstander', cursive;
      letter-spacing: 2px;
      border: none;
      border-radius: 5px;
      padding: 12px 25px;
      cursor: pointer;
    }
</style>
