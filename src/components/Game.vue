<template>
  <div>
    <header>
      <h1>Guess My Number!</h1>
      <div class="header-wrapper">
        <p class="between">(Between 1 and 20)</p>
        <button @click="resetTheGame" class="btn again">Again!</button>
      </div>
      <div class="number">{{ this.number }}</div>
    </header>

    <main>
      <section class="left">
        <input type="number" class="guess" v-model="guess" />
        <button @click="checkTheNumber" class="btn check">Check!</button>
      </section>
      <section class="right">
        <p class="message">{{ this.message }}</p>
        <p class="label-score">💯 Score: <span class="score">{{ this.score }}</span></p>
        <p class="label-highscore">
          🥇 Highscore: <span class="highscore">{{ highScore }}</span>
        </p>
      </section>
    </main>
  </div>

</template>

<script>
export default {
  data() {
    return {
      secretNumber: Math.trunc(Math.random() * 20) + 1,
      number: '?',
      guess: null,
      score: 20,
      highScore: 0,
      message: 'Start guessing...'
    }
  },

  methods: {
    checkTheNumber() {
      if (!this.guess) {
        this.message = '🤖 Enter a number!';

      } else if (+this.guess === this.secretNumber) {
        this.playerWins();

      } else if (+this.guess !== this.secretNumber) {
        this.guessIsWrong();
      }

      this.guess = null;
    },

    playerWins() {
      this.number = this.secretNumber;
      this.message = '😺 Correct Number!';

      document.querySelector('body').style.backgroundColor = '#60b347';
      document.querySelector('.number').style.width = '30rem';

      if (this.score > this.highScore) {
        this.highScore = this.score;
      }
    },

    guessIsWrong() {
    if (+this.guess <= 0) {
        this.message = 'Enter a number from 1 to 20';
      }

      else if (this.score > 1) {
        this.message = +this.guess > this.secretNumber ? '📈 Too high!' : '📉 Too low!';
        this.score--;
      }

      else {
        this.message = '🐒 Game Over';
        this.score = 0;
      }
    },

    resetTheGame() {
      this.score = 20;
      this.secretNumber = Math.trunc(Math.random() * 20) + 1;

      this.number = '?';
      this.message = 'Start guessing...';
      this.guess = null;
      document.querySelector('body').style.backgroundColor = '#222';
      document.querySelector('.number').style.width = '15rem';
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Press+Start+2P&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

html {
  font-size: 62.5%;
  box-sizing: border-box;
}

body {
  font-family: 'Press Start 2P', sans-serif;
  color: #eee;
  background-color: #222;
}

header {
  position: relative;
  height: 35vh;
  border-bottom: 7px solid #eee;
}

main {
  height: 65vh;
  color: #eee;
  display: flex;
  align-items: center;
  justify-content: space-around;
}

.left {
  width: 52rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.right {
  width: 52rem;
  font-size: 2rem;
}

h1 {
  font-size: 4rem;
  line-height: 4.5rem;
  text-align: center;
  position: absolute;
  width: 100%;
  top: 52%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.number {
  background: #eee;
  color: #333;
  font-size: 6rem;
  width: 15rem;
  padding: 3rem 0rem;
  text-align: center;
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translate(-50%, 50%);
}

.between {
  font-size: 1.4rem;
  position: absolute;
  top: 2rem;
  right: 2rem;
}

.again {
  position: absolute;
  top: 2rem;
  left: 2rem;
}

.guess {
  background: none;
  border: 4px solid #eee;
  font-family: inherit;
  color: inherit;
  font-size: 5rem;
  padding: 2.5rem;
  width: 25rem;
  text-align: center;
  display: block;
  margin-bottom: 3rem;
}

.btn {
  border: none;
  background-color: #eee;
  color: #222;
  font-size: 2rem;
  font-family: inherit;
  padding: 2rem 3rem;
  cursor: pointer;
}

.btn:hover {
  background-color: #ccc;
}

.message {
  margin-bottom: 8rem;
  line-height: 150%;
  height: 3rem;
  max-width: 40rem;
}

.label-score {
  margin-bottom: 2rem;
}


@media (max-width: 768px) {
  main {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .right {
    order: -1;
    margin-bottom: 35px;
    text-align: center;
    width: auto;
  }

  .left {
    width: auto;
  }

  .message {
    margin: 20px 0 35px 0;
  }
}

@media (max-width: 576px) {
  .header-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 30px;
  }

  .between {
    position: relative;
    top: 0;
    left: 0;
  }

  .again {
    position: relative;
    max-width: 300px;
    margin-top: 25px;
    top: 0;
    left: 0;
  }

  h1 {
    top: 165px;
    font-size: 36px;
    padding: 30px 0;
  }

  body .number {
    width: 130px;
    padding: 20px 0;
  }

  body {
    height: 100vh;
  }

  main {
    height: 480px;
  }

  header {
    height: 280px;
  }
}
</style>
