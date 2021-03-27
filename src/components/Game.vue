<template>
  <div class="game">
    <button @click="switchScreen()" class="test_button">TEST</button>
    <div class="game_screen_items" v-if="currentScreen === 'game'">
      <div class="data_component credits">
        <span>{{ credits }}</span>
      </div>
      <div class="data_component time">
        <span>{{ time }}</span>
      </div>
      <div class="data_component highscore">
        <span>{{ highscore }}</span>
      </div>
      <div v-if="isTwoPlayer" class="data_component highscore player_two">
        <span>{{ highscore }}</span>
      </div>
      <div class="data_component life">
        <span>{{ life }}</span>
      </div>
      <div class="score flex_wrap">{{ score }}</div>
    </div>
    <div class="game_screen_items" v-if="currentScreen === 'new high score'">
      <div class="flex_wrap">
        <div class="new_highscore_button">NEUER HIGHSCORE!!</div>
      </div>
    </div>
    <div class="game_screen_items" v-else-if="currentScreen === 'insert coin'">
      <div class="flex_wrap">
        <div class="insert_coin_text">
          Bitte GELD EINWERFEN <br />
          ODER GAME CARD SCANNEN
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Game",
  props: {
    msg: String,
  },
  data: function () {
    return {
      currentScreen: "new high score",
      isTwoPlayer: false,
      credits: 1,
      time: "00:30:00",
      highscore: 51,
      life: 2,
      score: 100,
    };
  },
  methods: {
    switchScreen: function () {
      switch (this.currentScreen) {
        case "game":
          this.currentScreen = "new high score";
          break;
        case "insert coin":
          this.currentScreen = "game";
          break;
        case "new high score":
          this.currentScreen = "insert coin";
          break;
        default:
          this.currentScreen = "insert coin";
          break;
      }
    },
  },
};
</script>

<style scoped lang="scss">
@keyframes comeIn {
  from {
    opacity: 0;
    transform: scale(0);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

@keyframes pulsating {
  from {
    transform: scale(0.7);
  }
  to {
    transform: scale(1.1);
  }
}

@keyframes pulsatingSmall {
  from {
    transform: scale(0.9);
  }
  to {
    transform: scale(1);
  }
}

@keyframes heartBeat {
  0% {
    transform: scale(1);
  }
  10% {
    transform: scale(0.9);
  }
  20% {
    transform: scale(1);
  }
  100% {
    transform: scale(1);
  }
}

.game {
  width: 100%;
  height: 100%;

  .test_button {
    z-index: 99;
    position: relative;
  }
  .game_screen_items {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;

    .flex_wrap {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 100%;
      height: 100%;
    }

    .new_highscore_button {
      background-image: url("./../assets/SVG/highscore cheer.svg");
      font-size: 150px;
      padding: 210px;
      background-repeat: no-repeat;
      color: #fff;
      background-position: center;
      animation: comeIn 0.5s 1, heartBeat 1s 0.5s infinite alternate;
    }

    .insert_coin_text {
      text-align: center;
      font-size: 100px;
      color: #fab612;
      -webkit-text-stroke-width: 1px;
      -webkit-text-stroke-color: #fff;
      text-shadow: 0px 0px 30px #000;
      line-height: 9rem;
      animation: pulsating 1.5s infinite alternate;
      // letter-spacing: 50px;
    }

    .score {
      text-align: left;
      font-size: 500px;
      color: #fab612;
      -webkit-text-stroke-width: 8px;
      -webkit-text-stroke-color: #fff;
      text-shadow: 0px 0px 30px #000;
      letter-spacing: 50px;
      animation: comeIn 0.4s 1 ease-in-out,
        pulsatingSmall 2s 0.5s infinite alternate ease-in-out;
    }

    .data_component {
      width: 500px;
      height: 180px;
      background-repeat: no-repeat;
      position: absolute;
      background-position: right;
      animation: comeIn 0.4s 1 ease-in-out;

      span {
        letter-spacing: 3px;
        color: #fff;
        position: absolute;
        font-size: 50px;
        right: 20px;
        bottom: 54px;
        width: 50%;
        text-align: center;
      }
    }
    .time {
      background-image: url("./../assets/SVG/time.svg");
      right: 50px;
      top: 20px;
    }
    .life {
      background-image: url("./../assets/SVG/life.svg");
      right: 50px;
      bottom: 20px;
    }
    .highscore {
      background-image: url("./../assets/SVG/highscore.svg");
      left: -10px;
      bottom: 20px;

      &.player_two {
        bottom: 220px !important;
      }
    }
    .credits {
      background-image: url("./../assets/SVG/credits.svg");
      left: -140px;
      top: 20px;

      span {
        width: 30%;
      }
    }
  }
}
</style>
