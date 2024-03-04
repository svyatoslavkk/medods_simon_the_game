<template>
  <select class="button" id="difficulty" v-model="selectedDifficulty">
    <option value="easy">Easy</option>
    <option value="normal">Normal</option>
    <option value="hard">Hard</option>
  </select>
</template>

<script>
export default {
  data() {
    return {
      selectedDifficulty: 'easy'
    };
  },
  watch: {
    selectedDifficulty() {
      this.$emit('difficultyChanged', this.selectedDifficulty);
    }
  }
};
</script>

<style>
  
</style>