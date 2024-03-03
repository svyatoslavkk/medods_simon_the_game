<template>
  <div id="app" class="app">
    <app-header></app-header>
    <app-stat></app-stat>
    <app-playground></app-playground>
  </div>
</template>

<script>
import header from './components/Header.vue';
import playground from './components/Playground.vue';
import stat from './components/Stat.vue';

export default {
  name: 'app',
  components: {
    'app-header': header,
    'app-playground': playground,
    'app-stat': stat,
  },
  data () {
    return {
      
    }
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  button {
    cursor: pointer;
  }
  .app {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 2rem;
    max-width: 750px;
    width: 100%;
  }
</style>
