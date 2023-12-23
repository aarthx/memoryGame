<script>
  export default {
    props: ['imageURL','dontLook'],
    emit: ['card-clicked'],
    methods: {
      cardClicked(e) {
        e.stopPropagation()
        if(!e.target.classList.contains('active')) {
          e.target.classList.add('active')
          this.$emit('card-clicked', e.target)
        }
      }
    }
  }
</script>

<template>
  <div :class="'flip-container ' + dontLook">
    <div @click="cardClicked" class="flipper">
      <div class="unique-card front">
        <img src="/card_verse.svg" alt="logo da card">
      </div>
      <div class="unique-card back">
        <img :src="imageURL" alt="logo da card">
      </div>
    </div>
  </div>
</template>

<style scoped>
  .flip-container {
    width: 10rem;
    height: 10rem;
    perspective: 1000px;
  }

  .flipper {
    cursor: pointer;
    position: relative;
    width: 100%;
    height: 100%;
    transform-style: preserve-3d;
    transition: transform 0.8s;
  }

  .flip-container .flipper.active, 
  .flip-container .flipper.permanent-active {
    transform: rotateY(180deg);
  }

  .front,.back {
    pointer-events: none;
    position: absolute;
    width: 100%;
    height: 100%;
    backface-visibility: hidden;
  }

  .back {
    transform: rotateY(180deg);
  }

  .unique-card {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 10rem;
    height: 10rem;
    background: linear-gradient(180deg, rgba(124,223,100,1) 0%, rgba(100,135,103,1) 100%);
    box-shadow: inset 0 0 0px 8px var(--color-primary);
    cursor: pointer;
    transition: ease-in-out 0.5s;
    overflow: hidden;
  }

  .flipper:hover {
    background: var(--color-secundary);
    transform: rotate(5deg);
    transition: ease-in-out 0.5s;
  }

  .unique-card.front img {
    pointer-events: none;
    width: 50%;
  }

  .unique-card.back img {
    width: 90%;
    box-shadow: inset 0 0 0px 8px var(--color-primary);
    pointer-events: none;
    object-fit: contain;
  }

  .unique-card.active {
    background: red;
  }

  @media(max-width: 550px) {
    .flip-container, .unique-card {
      width: 8rem;
      height: 8rem;
    }
  }

  @media(max-width: 450px) {
    .flip-container, .unique-card {
      width: 7rem;
      height:7rem;
    }
  }

  @media(max-width: 350px) {
    .flip-container, .unique-card {
      width: 6rem;
      height: 6rem;
    }
  }
</style>