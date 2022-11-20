<template>
  <div id="app">
    <div class="wrapper clearfix">
      <Players
        :scoresPlayerChild="scoresPlayer"
        :currentScore="currentScore"
        :activePlayer="activePlayer"
      />
      <!-- v-on:handleNewGame: tên sự kiện  -->
      <!-- handleNewGame(): tên function  -->
      <Controls 
      v-on:handleNewGame="handleNewGame()" 
      v-on:rollDice="rollDice()"
      v-on:handleHoldScore="handleHoldScore()"
      />
      <Dices :dices="dices"/>
      <PopupRule
        v-on:handleConfirm="handleConfirm"
        :isOpenPopUp="isOpenPopUp"
      />
    </div>
  </div>
</template>

<script>
import Controls from "./components/Controls.vue";
import Dices from "./components/Dices.vue";
import Players from "./components/Players.vue";
import PopupRule from "./components/PopupRule";
export default {
  name: "app",
  data() {
    return {
      scoresPlayer: [33, 44],
      currentScore: 27,
      activePlayer: 1,
      isOpenPopUp: false,
      isPlaying: false,
      dices: [3, 5]
    };
  },
  components: {
    Players,
    Controls,
    Dices,
    PopupRule
  },
  methods: {
    handleConfirm() {
      console.log("App Vue");
      this.isOpenPopUp = false;
      this.isPlaying = true;
      this.activePlayer = 0;
      this.currentScore = 0;
      this.scoresPlayer = [0, 0];
      this.dices = [6, 6];
    },
    handleNewGame() {
      console.log("New game from App.vue");
      //Hiển thị pop up -> show luật chơi
      this.isOpenPopUp = true;
      console.log(this.isOpenPopUp);
    },
    rollDice() {
        console.log('App vue roll dice');
        if(this.isPlaying) {
            // xoay súc xắc
            let dice1 = Math.floor(Math.random() * 6) + 1
            let dice2 = Math.floor(Math.random() * 6) + 1
            this.dices= [dice1, dice2]
            if(dice1 === 1 || dice2 === 1) {
                setTimeout(()=>{
                    alert(`Trúng 1 gòi. Đổi lượt chơi nhé player ${this.activePlayer + 1}`)
                }, 200)
                this.nextPlayer()
            } else {
                // Cộng dồn điểm tạm thời
                this.currentScore = this.currentScore + dice1 + dice2 
            }
        } else alert('Chưa chơi mà bấm xoay gì ba...Bấm chơi đi.')
    },
    nextPlayer(){
        // Đổi lượt chơi
        this.activePlayer = this.activePlayer === 0 ? 1 : 0
        // Reset điểm tạm thời về 0
        this.currentScore = 0
    },
    handleHoldScore(){
        if(this.isPlaying) {

            console.log(1234);
            console.log(this);
            let {scoresPlayer, activePlayer, currentScore} = this
            let oldScore = scoresPlayer[activePlayer]
            // Cách 1: Sử dụng set để thay đổi giá trị của ô nhớ
            // let scoreAfterClickHoldOn = oldScore + currentScore
            // this.$set(this.scoresPlayer, activePlayer, scoreAfterClickHoldOn)
            
            // Cách 2: Thay đổi địa chỉ ô nhớ để Vue phàn ứng lại với giao diện
            let cloneScorePlayer = [...scoresPlayer]
            cloneScorePlayer[activePlayer] = oldScore + currentScore
            this.scoresPlayer = cloneScorePlayer

            this.nextPlayer()
        } else alert('Chưa chơi mà bấm xoay gì ba...Bấm chơi đi.')
    }
  }
};
</script>

<style>
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
    url("/public/assets/back.jpg");
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
