<script>
  import Card from './Card.vue'

  export default {
    data() {
      return {
        isMounted: false
      }
    },
    emits: ['test-win'],
    props: ['allCards'],
    components: {
      'card': Card
    },
    methods: {
      shuffleCards() {
        let lista = document.getElementById('cardsList')

        let elements = Array.from(lista.children);

        elements.sort(function () {
          return Math.random() - 0.5;
        });

        lista.innerHTML = '';
        elements.forEach(function (element) {
          lista.appendChild(element);
        });
      },
      testCorrect(e) {
        let activedElements = []
        let lista = document.getElementById('cardsList').children
        for(let i = 0; i < lista.length; i++) {
          if(lista[i].firstChild.classList.contains('active')) {
            activedElements.push(lista[i])
          }
        }

        if(activedElements.length >= 2) {
          document.getElementById('blockScreen').style.display = 'block';
          if(activedElements[0].classList[1] === activedElements[1].classList[1]) {
            activedElements[0].firstChild.classList.add('permanent-active')
            activedElements[0].firstChild.classList.remove('active')
            activedElements[1].firstChild.classList.add('permanent-active')
            activedElements[1].firstChild.classList.remove('active')
            document.getElementById('blockScreen').style.display = 'none';
            setTimeout(() => {
              this.testWin()
            }, 500)
          } else {
            setTimeout(() => {
              for (let i = 0; i < lista.length; i++) {
                if (lista[i].firstChild.classList.contains('active')) {
                  lista[i].firstChild.classList.remove('active')
                }
              }
              document.getElementById('blockScreen').style.display = 'none';
            }, 1000)
          }
        }
      },
      testWin() {
        let lista = document.getElementById('cardsList').children
        lista = Array.from(lista)
        let venceu = lista.every(el => el.firstChild.classList.contains('permanent-active'))
        if(venceu) {
          this.$emit('test-win')
        }
      }
    },
    mounted() {
      this.isMounted = true;
      this.shuffleCards()
    },
  }
</script>

<template>
  <TransitionGroup mode="out-in" tag="div" class="cards-deck" id="cardsList">
    <card v-for="x in allCards" :key="x" v-show='isMounted' :imageURL="'https://source.unsplash.com/random/200x200?sig='+ x" :dontLook="x" @card-clicked="testCorrect"/>
    <card v-for="x in allCards" :key="x" v-show='isMounted' :imageURL="'https://source.unsplash.com/random/200x200?sig='+ x" :dontLook="x" @card-clicked="testCorrect"/>
  </TransitionGroup>
  <div id="blockScreen"></div>
</template>

<style scoped>
  .cards-deck {
    display: flex;
    flex-wrap: wrap;
    gap: 2rem;
    align-items: center;
    justify-content: center;
  }
  .v-enter-from {
  opacity: 0;
  translate: -200px 0;
  }
  .v-enter-to {
    opacity: 1;
    translate: 0 0;
  }
  .v-enter-active,
  .v-leave-active {
    transition: all 0.7s;
  }
  
  #blockScreen {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: none;
    z-index: 9999;
  }

  @media(max-width: 800px) {
    .cards-deck {
      margin: 1rem 0;
    }
  }

  @media(max-width: 430px) {
    .cards-deck {
      gap: 0.5rem;
    }
  }

</style>