<template>
  <div class="oo">
    <div class="game" @click="ClickOnInterface" :class="{wait: !player || stopped}">
      <span class="time" v-if="!stopped">{{ time }}</span>
      <span v-if="player && !stopped" class="round"
      :class="{ bonus: bonusActivated, badColor: badColorActivated }"
      :style="roundStyle"
      @click.stop="ClickOnRound"
      @click.alt.stop="bonus"></span>
    </div>
    <div class="log">
      <!-- <p v-for="item in userLogs">#{{ item.id }} : {{ item.message }}</p> -->
    </div>
  </div>
</template>

<script>
export default {
  name: 'Game',
  props: ['player'],
  data: function () {
    return {
      click: 0,
      time: 0,
      roundStyle: {
        width: '50px',
        height: '50px',
        margin: '20% 20%'
      },
      bonusActivated: false,
      badColorActivated: false,
      collection: [],
      stopped: true
    }
  },
  computed: {
    userLogs: function () {
      return this.collection.filter(function (item) {
        return item.type === 'user'
      })
    }
  },
  created: function () {
    document.onkeydown = this.start
  },
  watch: {
    click: function () {
      this.updateRound()
      this.$emit('score', this.click)
    },
    player: function () {
      this.stopped = false
      this.time = 10

      let self = this
      setInterval(function () {
        self.updateTime()
      }, 1000)
    }
  },
  methods: {
    updateTime: function () {
      if (this.time === 0) {
        this.stopped = true
      }

      if (!this.stopped) {
        this.time--
      }
    },
    ClickOnRound: function (event) {
      setTimeout(this.updateRound, 1000)

      this.updateClick(true)
      this.addLog(`BRAVO !`)
    },
    bonus: function (event) {
      if (this.bonusActivated) {
        this.updateClick(true)
        this.addLog(`PERFECT ! +2`)
      } else {
        this.updateClick()
        this.addLog(`BRAVO ! -1`)
      }
    },
    ClickOnInterface: function (event) {
      this.updateClick()
      this.addLog(`OH NON :( -1`)
    },
    updateClick: function (increment) {
      if (!this.player || this.stopped) {
        return
      }

      if (increment) {
        this.click++
      } else {
        this.click--
      }
    },
    start: function (event) {
      if (event.key === 'Enter') {
        console.log('START')
      }
    },
    updateRound: function () {
      let size = Math.random() * (100 - 10) + 10
      let top = Math.random() * (55 - 5) + 5
      let left = Math.random() * (55 - 5) + 5

      this.roundStyle.height = this.roundStyle.width = `${size}px`
      this.roundStyle.margin = `${top}% ${left}%`

      this.badColorActivated = size < 20
      this.bonusActivated = size > 80

      this.addLog({
        size: size,
        top: top,
        left: left
      }, 'round')
    },
    addLog: function (message, type) {
      if (!this.player || this.stopped) {
        return
      }

      let typeOfMessage = type || 'user'
      this.collection.unshift({id: this.collection.length / 2, message: message, type: typeOfMessage})
    }
  }
}
</script>

<style scoped>
  .oo {
    height: 530px;
  }

  .game {
    position: relative;
    width: 100%;
    height: 90%;
    display: block;
    background: #9c89b8;
    opacity: 1;
    transition: opacity 1s;
  }

  /* .log {
    width: 100%;
    height: 50px;
    background: #666;
    display: block;
  } */

  .round {
    background: rgb(152, 173, 192);
    border-radius: 9999px;
    position: absolute;
    transition: width 2s, height 2s, margin 0.5s;
  }

  .bonus {
    background: #c93636;
  }

  .badColor {
    background: #2A4747;
  }

  .wait {
    opacity: 0.3;
  }

  .time {
    position: absolute;
    font-size: 90pt;
    padding-left: 30px;
    color: aliceblue;
    opacity: 0.2;
  }
</style>
