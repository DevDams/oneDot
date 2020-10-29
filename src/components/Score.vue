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
    margin-top: 10px;
    text-align: center;
    font-weight: bolder;
    color: #f870b2;
    /* display:block;
    height:50px;
    width:105px;
    font-size:19pt;
    font-weight:600;
    background:#000;
    padding:5px;
    line-height:40px;
    margin:0 auto; */
  }
</style>
