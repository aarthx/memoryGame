<script>
  import Button from './Button.vue'

export default {
  data() {
    return {
      btnOptions: [
        { name: 'Fácil (10)', active: true, cards: 5 },
        { name: 'Médio (20)', active: false, cards: 10 },
        { name: 'Dificil (32)', active: false, cards: 16 },
        { name: 'Nightmare (40)', active: false, cards: 20 }
      ],
      totalCards: 2
    }
  },
  props: ['allCards'],
  components: {
    'custom-btn': Button
  },
  watch: {
    totalCards(newVal) {
      this.$emit('total-cards', newVal)
    }
  },
  emits: ['change-menu', 'total-cards'],
  methods: {
    toggleDiff(e) {
      for (let i = 0; i < this.btnOptions.length; i++) {
        if (e.target.innerText === this.btnOptions[i].name && this.btnOptions[i].active === false) {
          this.btnOptions[i].active = true
          this.totalCards = this.btnOptions[i].cards
        } else if(e.target.classList.contains('active')) {
          
        } else {
          this.btnOptions[i].active = false
        }
      }
    },
    changeMenu() {
      this.$emit('change-menu')
    }
  }
}
</script>

<template>
  <p class="main-text"><b>Bem vindo</b> ao jogo da memória<br>
  Escolha o nivel de dificuldade:</p>
  <div class="diff-options">
    <custom-btn 
      v-for="x in btnOptions"
      :key="x.name"
      :button-name="x.name"
      :class="{ active: x.active }"
      @click="toggleDiff"
    />
  </div>
  <custom-btn @click="changeMenu" class="btn-jogar" button-name="JOGAR"/>
</template>

<style scoped>
  .main-text {
    font-size: 3rem;
    text-align: center;
  }

  .diff-options {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 1rem;
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
  .v-enter-from {
    opacity: 0;
    rotate: 180deg;
  }
  .v-enter-to {
    opacity: 1;
    rotate: 0deg;
  }
  .v-enter-active {
    transition: all 0.7s;
  }

  @media (max-width: 1030px) {
    .btn-jogar,.diff-options {
      text-align: center;
    }
  }

  @media (max-width: 800px) {
    .diff-options {
      flex-wrap: wrap;
    }
    .btn-jogar,.diff-options {
      margin: 2rem 0;
    }
  }

  @media (max-width:680px) {
    .main-text {
      font-size: 2rem;
      text-align: center;
    }
  }

  @media (max-width: 430px) {
    .diff-options {
      font-size: 1rem ;
    }
  }

</style>