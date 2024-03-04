<template>
  <section id="playground" class="playground">
    <button
      v-for="(color, index) in colors"
      :key="index"
      class="play-button"
      :style="{ backgroundColor: color }"
      @click="buttonClicked(color)"
      :class="{ active: activeColors.includes(color) }"
    ></button>
  </section>
</template>

<script>
export default {
  props: {
    colors: Array,
    playSound: Function,
    sounds: Object
  },
  data() {
    return {
      activeColors: [],
    };
  },
  methods: {
    buttonClicked(color) {
      this.$emit('clicked', color);
      this.activate(color);
      this.playSound(color);
    },
    activate(color) {
      this.activeColors.push(color);
      this.playSound(color);
      setTimeout(() => {
        const index = this.activeColors.indexOf(color);
        if (index !== -1) {
          this.activeColors.splice(index, 1);
        }
      }, 500);
    },
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
    opacity: 0.5;
    transition: 0.1s ease;
  }
  .play-button:hover {
    opacity: 0.9;
  }
  .active {
    opacity: 1;
    border: 3px solid #111;
  }
</style>