<template>
  <header class="header">
    <button class="button">Start Game</button>
    <button class="button">Reset Game</button>
    <select class="button">
      <option value="easy">Easy</option>
      <option value="normal">Normal</option>
      <option value="hard">Hard</option>
    </select>
  </header>
</template>

<script>

</script>

<style>
  .header {
    display: flex;
    justify-content: space-around;
    width: 100%;
  }
  .button {
    border-radius: 0.5rem;
    border: none;
    outline: none;
    padding: 0.5rem 1rem;
    background-color: rgb(53, 60, 255);
    color: #eee;
    font-weight: 800;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    font-size: 18px;
  }
</style>