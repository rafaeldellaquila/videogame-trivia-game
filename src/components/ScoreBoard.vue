<template>
  <section class="score">
    Player <span>{{ this.winCount }}</span>
    x
    <span>{{ this.loseCount }}</span> Computer
  </section>
</template>

<script>
export default {
  name: 'ScoreBoard',
  props: ['winCount', 'loseCount']
}
</script>

<style lang="scss" scoped>
.score {
  border-bottom: 1px solid black;
  padding: 24px;
  font-size: 18px;
  span {
    padding: 8px;
    border-bottom: 1px solid black;
    font-weight: bold;
  }
}
</style>
