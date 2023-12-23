<script>
  export default {
    props: [
      'buttonName'
    ]
  }
</script>

<template>
  <button ref="btn">{{ buttonName }}</button>
</template>

<style scoped>
  button {
    all: unset;
    border-radius: 5px;
    font-size: 2rem;
    background-color: var(--color-secundary);
    padding: 0 1rem;
    box-shadow: 0 4px 4px 0px rgba(0, 0, 0, 0.25);
    cursor: pointer;
  }

  button:hover {
    background-color: #9CDF64;
    box-shadow: 0 4px 4px 0px rgba(0, 0, 0, 0.25);
  }

  button.active {
    box-shadow: inset 0 0 0 5px var(--color-primary)
  }
</style>