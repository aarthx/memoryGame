<script>
  import Button from './Button.vue'

  export default {
    components: {
      'custom-btn': Button
    },
    emits: ['comeback'],
    methods: {
      comeback() {
        this.$emit('comeback')
      }
    }
  }
  
</script>

<template>
  <p class="main-text"><b>PARABÉNS</b> você venceu!!!</p>
  <div class="final-btns">
    <custom-btn @click="comeback" class="btn-jogar" button-name="Jogar Novamente"/>
    <a href="https://aarthx.github.io/" target="_blank"><custom-btn class="btn-conhecer" button-name="Conheça outros projetos"/></a>
  </div>
</template>

<style scoped>
  .main-text {
    font-size: 3rem;
    text-align: center;
  }

  .final-btns {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2rem;
  }

  .btn-jogar {
    background-color: var(--color-primary);
    font-size: 2.5rem;
    font-weight: bold;
    margin: 4rem 0 0 0;
  }
  .btn-jogar:hover {
    background-color: var(--color-secundary);
    font-size: 2.5rem;
  }
  .btn-jogar:active {
    box-shadow: none;
  }

  a {
    text-decoration: none;
    color: black;
  }

  @media(max-width: 800px) {
    .final-btns{
      margin: 2rem 0;
    }
    .btn-jogar{
      margin: 0;
    }
  }

  @media(max-width: 400px) {
    .final-btns{
      text-align: center;
    }

  }

</style>