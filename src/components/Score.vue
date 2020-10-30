<template>
    <div class="score" v-if="player">
        {{ score }}
    </div>
</template>

<script>
export default {
  name: 'Score',
  props: ['score', 'player']
}
</script>

<style scoped>
  .score {
    text-align: center;
    font-weight: bolder;
    color: #f2f2f2;
    display:block;
    height:50px;
    width:85px;
    font-size:19pt;
    font-weight:600;
    font-family: 'Grandstander', cursive;
    background:#000;
    line-height:50px;
    margin:10px auto;
  }
</style>
