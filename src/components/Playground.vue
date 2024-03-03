<template>
  <section id="playground" class="playground">
    <button v-for="(color, index) in colors" :key="index" class="play-button" :style="{ backgroundColor: color }"></button>
  </section>
</template>

<script>
export default {
  data() {
    return {
      colors: ['red', 'green', 'blue', 'greenyellow'],
    };
  },
  methods: {
    
  }
};
</script>

<style>
  .playground {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
    max-width: 244px;
    margin: 0 auto;
  }
  .play-button {
    width: 128px;
    height: 128px;
    border: none;
    border-radius: 0.5rem;
    opacity: 0.66;
    transition: 0.1s ease;
  }
  .play-button:hover {
    opacity: 1;
  }
</style>