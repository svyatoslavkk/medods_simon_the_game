<template>
  <div id="app" class="app">
    <div>
      <button class="button" @click="toggleGame">{{ gameInProgress ? 'Reset Game' : 'Start Game' }}</button>
    </div>
    <SelectLevel @difficultyChanged="changeDifficulty" />
    <Stat :score="score" />
    <Playground 
      :colors="colors" 
      @clicked="handleButtonClick" 
      :playSound="playSound" 
      :sounds="sounds"
    />
    <audio v-for="(color, index) in colors" :ref="`${color}Sound`" :key="index" :src="`/src/assets/${color}.mp3`"></audio>
  </div>
</template>

<script>
import SelectLevel from './components/SelectLevel.vue';
import Playground from './components/Playground.vue';
import Stat from './components/Stat.vue';

export default {
  name: 'app',
  components: {
    SelectLevel,
    Playground,
    Stat,
  },
  data () {
    return {
      colors: ['red', 'green', 'blue', 'gold'],
      sequence: [],
      userSequence: [],
      score: 0,
      gameInProgress: false,
      difficulty: 'easy',
      interval: {
        easy: 1500,
        normal: 1000,
        hard: 400
      },
      sounds: {}
    }
  },
  mounted() {
    this.colors.forEach(color => {
      this.sounds[color] = this.$refs[`${color}Sound`][0];
      this.sounds[color].load();
    });
  },
  methods: {
    toggleGame() {
      if (this.gameInProgress) {
        this.resetGame();
      } else {
        this.startGame();
      }
    },
    startGame() {
      this.gameInProgress = true;
      this.sequence = [];
      this.userSequence = [];
      this.score = 0;
      this.nextSequence();
    },
    resetGame() {
      this.gameInProgress = false;
      this.sequence = [];
      this.userSequence = [];
      this.score = 0;
    },
    handleButtonClick(color) {
      if (this.gameInProgress) {
        this.userSequence.push(color);
        this.checkSequence();
      }
    },
    nextSequence() {
      const nextColor = this.colors[Math.floor(Math.random() * this.colors.length)];
      this.sequence.push(nextColor);
      this.playSequence(0);
    },
    playSequence(index) {
      if (index < this.sequence.length) {
        setTimeout(() => {
          this.activateButton(this.sequence[index]);
          this.playSound(this.sequence[index]);
          this.playSequence(index + 1);
        }, this.interval[this.difficulty]);
      } else {
        this.userSequence = [];
      }
    },
    checkSequence() {
      for (let i = 0; i < this.userSequence.length; i++) {
        if (this.userSequence[i] !== this.sequence[i]) {
          this.gameOver();
          return;
        }
      }
      if (this.userSequence.length === this.sequence.length) {
        this.score++;
        setTimeout(() => {
          this.nextSequence();
        }, 1000);
      }
    },
    gameOver() {
      alert('Game Over! Your score: ' + this.score);
      this.gameInProgress = false;
    },
    activateButton(color) {
      const button = document.querySelector(`.play-button[style*="${color}"]`);
      if (button) {
        button.classList.add('active');
        setTimeout(() => {
          button.classList.remove('active');
        }, 500);
      }
    },
    changeDifficulty(newDifficulty) {
      this.difficulty = newDifficulty;
    },
    playSound(color) {
      if (this.sounds[color]) {
        this.sounds[color].currentTime = 0;
        this.sounds[color].play();
      }
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