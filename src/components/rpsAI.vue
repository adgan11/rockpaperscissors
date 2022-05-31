<template>
  <div class="main">
    <button v-if="showButtons"><img @click="actionSelected(0)" id="chooseButton" :src="rockImgSmall" /></button>
    <button v-if="showButtons"><img @click="actionSelected(1)" id="chooseButton" :src="paperImgSmall" /></button>
    <button v-if="showButtons"><img @click="actionSelected(2)" id="chooseButton" :src="scissorsImgSmall" /></button>
    <hr>
    <img align="left" :class="leftRockClass" :src= "myCurrentImg" />
    <img align="right" :class="rightRockClass" :src= "enemyCurrentImg" />

    <h1 class="pp">{{ playerPoints }}</h1> <h1 class="ep">{{ enemyPoints }}</h1>
    

  </div>

</template>

<script>
export default {
  name: 'rpsAI',
  data() {
    return {
      rockImgSmall: "https://img.icons8.com/stickers/100/000000/hand-rock-skin-type-3.png",
      paperImgSmall: "https://img.icons8.com/stickers/100/000000/hand-skin-type-3.png",
      scissorsImgSmall: "https://img.icons8.com/stickers/100/000000/hand-scissors-skin-type-3.png",
      rockImg: "https://img.icons8.com/stickers/300/000000/hand-rock-skin-type-3.png",
      paperImg: "https://img.icons8.com/stickers/300/000000/hand-skin-type-3.png",
      scissorsImg: "https://img.icons8.com/stickers/300/000000/hand-scissors-skin-type-3.png",
      rightRockClass: "rotate-90",
      leftRockClass: "rotate90",
      myCurrentImg: "https://img.icons8.com/stickers/300/000000/hand-rock-skin-type-3.png",
      enemyCurrentImg: "https://img.icons8.com/stickers/300/000000/hand-skin-type-3.png",
      myHand: "rock",
      enemyHand: "rock",
      enemyChooseOptions: ["rock", "paper", "scissors"],
      playerPoints: 0,
      enemyPoints: 0,
      showButtons: true,
    }
  },
  methods: {
    actionSelected(index) {
      if (index === 0) {
        this.leftRockClass = "rotate90";
        this.myCurrentImg = this.rockImg;
        this.myHand = "rock";
      }
      else if (index === 1) {
        this.leftRockClass = "rotate90";
        this.myCurrentImg = this.paperImg;
        this.myHand = "paper";
      }
      else {
        this.leftRockClass = "no-flip";
        this.myCurrentImg = this.scissorsImg;
        this.myHand = "scissors";
      }
      console.log(this.myHand);
      this.enemyTurn();
    },
    async enemyTurn() {
      let randomChoice = this.enemyChooseOptions[Math.floor(Math.random() * this.enemyChooseOptions.length)];
      console.log("Enemy Chose: " + randomChoice);
      if (randomChoice === "rock") {
        this.enemyCurrentImg = this.rockImg;
        this.rightRockClass = "rotate-90";
        if (this.myHand === "rock") {
          console.log("Tie!");
        }
        else if (this.myHand === "paper") {
          console.log("Player Won!");
          this.playerPoints += 1;
        }
        else {
          console.log("Enemy Won!");
          this.enemyPoints += 1;
        }
      }
      else if (randomChoice === "paper") {
        this.enemyCurrentImg = this.paperImg;
        this.rightRockClass = "rotate-90";
        if (this.myHand === "rock") {
          console.log("Enemy Won!");
          this.enemyPoints += 1;
        }
        else if (this.myHand === "paper") {
          console.log("Tie!");
        }
        else {
          console.log("Player Won!");
          this.playerPoints += 1;
        }
      }
      else {
        this.enemyCurrentImg = this.scissorsImg;
        this.rightRockClass = "flip-only";
        if (this.myHand === "rock") {
          console.log("Player Won!");
          this.playerPoints += 1;
        }
        else if (this.myHand === "paper") {
          console.log("Enemy Won!");
          this.enemyPoints += 1;
        }
        else {
          console.log("Tie!");
        }
      }
      this.showButtons = false;

      const delay = ms => new Promise(res => setTimeout(res, ms));

      await delay(2000);
      this.leftRockClass = "rotate90";
      this.myCurrentImg = this.rockImg;
      this.rightRockClass = "rotate-90";
      this.enemyCurrentImg = this.rockImg;
      this.showButtons = true;
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .main {
    background: rgba(17, 24, 39, 1);
    position:absolute;
    top:0px;
    right:0px;
    bottom:0px;
    left:0px;
    text-align: center;
    padding-top: 30px;
    overflow: hidden;
  }
  h1 {
    color: white;
  }
  .rotate-90 {
    transform: rotate(-90deg) scaleX(-1);
    margin-top: 150px;
    animation: hand-move-right 0.3s;
    animation-iteration-count: infinite;
  }
  .rotate90 {
    transform: rotate(90deg) scaleX(1);
    margin-top: 150px;
    animation: hand-move-left 0.3s;
    animation-iteration-count: infinite;
  }
  .flip-only {
    transform: scaleX(-1);
    margin-top: 150px;
    animation: hand-move-right-flip-only 0.3s;
    animation-iteration-count: infinite;
  }
  .no-flip {
    transform: rotate(0deg);
    margin-top: 150px;
    animation: hand-move-left-no-flip 0.3s;
    animation-iteration-count: infinite;
  }
  .pp {
    color: green;
    float: left;
  }
  .ep {
    color: red;
    float: right;
  }
  @keyframes hand-move-left {
    0% {
      transform: rotate(88deg) scaleX(1)
    }
    50% {
      transform: rotate(90deg) scaleX(1);
    }
    100% {
      transform: rotate(92deg) scaleX(1)
    }
  }
  @keyframes hand-move-left-no-flip {
    0% {
      transform: rotate(-2deg) scaleX(1);
    }
    50% {
      transform: rotate(0deg) scaleX(1);
    }
    100% {
      transform: rotate(2deg) scaleX(1);
    }
  }
  @keyframes hand-move-right-flip-only {
    0% {
      transform: rotate(-2deg) scaleX(-1)
    }
    50% {
      transform: rotate(0deg) scaleX(-1);
    }
    100% {
      transform: rotate(2deg) scaleX(-1)
    }
  }
  @keyframes hand-move-right {
    0% {
      transform: rotate(-88deg) scaleX(-1)
    }
    50% {
      transform: rotate(-90deg) scaleX(-1);
    }
    100% {
      transform: rotate(-92deg) scaleX(-1)
    }
  }

</style>
