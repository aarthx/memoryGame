<script>
  import StartSet from './components/StartSet.vue'
  import GameSet from './components/GameSet.vue'
  import GameEnd from './components/GameEnd.vue'
  export default {
    data() {
      return {
        curMenu: 'start-set',
        totalCards: 5
      }
    },
    components: {
      'start-set': StartSet,
      'game-set': GameSet,
      'game-end': GameEnd,
    },
    methods: {
      setChange() {
        this.curMenu = 'game-set'
      },
      changeTotalCards(newVal) {
        this.totalCards = newVal
      },
      setFinish() {
        this.curMenu = 'game-end'
      },
      setStart() {
        this.curMenu = 'start-set'
      }
    }
  }
</script>

<template>
  <h1>Memory Game</h1>
  <main>
    <start-set @changeMenu="setChange" @totalCards="changeTotalCards" v-if="curMenu === 'start-set'"/>
    <game-set @test-win="setFinish" :allCards="totalCards" v-else-if="curMenu === 'game-set'"/>
    <game-end @comeback="setStart" v-else-if="curMenu === 'game-end'"/>
  </main>
</template>

<style scoped>
  h1 {
    font-family: var(--font-special);
    font-size: 5rem;
    color: white;
    text-align: center;
    font-weight: normal;
  }

  main {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 5rem 5rem;
    width: 80%;
    margin: 0 auto;
    background-color: var(--color-bg);
    border-radius: 5px;
  }
  
  @media (max-width: 800px) {
    main {
      width: 100%;
      padding: 0rem 1rem;
      border-radius: 0;
    }
  }

  @media (max-width: 460px) {
    h1 {
      font-size: 3rem;
      text-align: center;
    }
  }

</style>
