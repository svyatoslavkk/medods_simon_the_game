<template>
  <div class="game__over">
    <div class="modal">
      <h2>Game Over!</h2>
      <h3>Your score: {{ score }}</h3>
      <button class="button" @click="continueClicked">Continue</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    score: Number
  },
  methods: {
    continueClicked() {
      this.$emit('continueClicked');
    }
  }
};
</script>

<style>
.game__over {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: rgba(10, 10, 10, 0.6);
  z-index: 100;
}
.modal {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  gap: 1rem;
  align-items: center;
  background-color: #eee;
  padding: 3rem;
}
</style>