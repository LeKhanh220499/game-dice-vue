<template>
  <div id="app">
    <div class="wrapper clearfix">
      <player
        v-bind:scorePlayer="scorePlayer"
        v-bind:scoreCurrent="scoreCurrent"
        v-bind:activePlayer="activePlayer"
      >
      </player>

      <control
        v-on:handleNewGame="handleNewGame"
        v-on:handleRollDice="handleRollDice"
        v-on:handleHoldScore="handleHoldScore"
        v-on:handleFinalScore="handleFinalScore"
      >
      </control>

      <dice v-bind:dices="dices"></dice>

      <popup-rule
        v-bind:activePop="activePop"
        v-on:handleConfirm="handleConfirm"
      >
      </popup-rule>
    </div>
  </div>
</template>

<script>
import Player from "./components/Player.vue";
import Control from "./components/Control.vue";
import Dice from "./components/Dice.vue";
import PopupRule from "./components/PopupRule.vue";

export default {
  name: "app",
  data() {
    return {
      scorePlayer: [30, 40],
      scoreCurrent: 30,
      activePlayer: 1,
      isPlaying: false,
      activePop: false,
      dices: [5, 5],
    };
  },
  components: {
    Player,
    Control,
    Dice,
    PopupRule,
  },
  methods: {
    handleNewGame() {
      this.activePop = true;
    },
    handleConfirm() {
      (this.activePop = false),
        (this.isPlaying = true),
        (this.activePlayer = 1),
        (this.scoreCurrent = 0),
        (this.scorePlayer = [0, 0]),
        (this.dices = [1, 1]);
    },

    nextPlayer() {
      this.activePlayer = this.activePlayer === 1 ? 2 : 1;
      this.scoreCurrent = 0;
    },

    handleRollDice() {
      if (this.isPlaying) {
        var dice1 = Math.floor(Math.random() * 6 + 1);
        var dice2 = Math.floor(Math.random() * 6 + 1);

        this.dices = [dice1, dice2];

        console.log(dice1, dice2);
        if (dice1 == 1 || dice2 == 1) {
          let activePlayer = this.activePlayer;
          setTimeout(function () {
            console.log(this);
            alert(`Người chơi Player ${activePlayer} đã quay trúng vào số 1`);
          }, 10);
          this.nextPlayer();
        } else {
          this.scoreCurrent = this.scoreCurrent + dice1 + dice2;
        }
      } else {
        alert("Vui lòng nhấn vào nút NewGame");
      }
    },

    handleHoldScore() {
      if (this.isPlaying) {
        let { scorePlayer, scoreCurrent, activePlayer } = this;
        let scoreOld = scorePlayer[activePlayer - 1];
    
        // this.scorePlayer[activePlayer - 1] = scoreOld + scoreCurrent;
        this.$set(this.scorePlayer, activePlayer -1 , scoreOld + scoreCurrent )

        // setTimeout(function () {
        //   console.log(this);
        //   alert(`Người chơi Player ${activePlayer} đã hold`);
        // }, 10);
        this.nextPlayer();

      } else {
        alert("Vui lòng nhấn vào nút NewGame");
      }
    },

    handleFinalScore(){
      
    }
  },
};
</script>

<style>
/**********************************************
*** GENERAL
**********************************************/

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

body {
  background-image: linear-gradient(
      rgba(62, 20, 20, 0.4),
      rgba(62, 20, 20, 0.4)
    ),
    url(/public/assets/back.jpg);
  background-size: cover;
  background-position: center;
  font-family: Lato;
  font-weight: 300;
  position: relative;
  height: 100vh;
  color: #555;
}

.wrapper {
  width: 1000px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}
</style>
