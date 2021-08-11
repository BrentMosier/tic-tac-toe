<template>
  <div>
    <v-app-bar color="info" density="compact">
      <v-app-bar-title>Tic-Tac-Toe</v-app-bar-title>
    </v-app-bar>
    <div>
      <div  class=text-center style="padding-top:50px; padding-bottom:50px">
        <h2>You are X's. Play Tic-Tac-Toe to beat the computer.</h2>
      </div>
      <v-container>
        <v-row>
          <v-col v-for="(item, ind) in plays" :key="ind" cols="4">
            <board-space v-bind:move="item" v-bind:index="ind" @clicked="onButtonClick"/>
          </v-col>
        </v-row>
        <v-row>
          <v-col  class=text-center style="padding-top:50px; padding-bottom:50px">
            <h1>{{resultText}}</h1>
          </v-col>
        </v-row>
        <v-row justify="center">
            <v-btn color="primary" block @click="resetBoard"> Play Again</v-btn>
        </v-row>
      </v-container>
    </div>
  </div>
</template>

<script>
import BoardSpace from './BoardSpace.vue';
export default {
  components: { BoardSpace },
  name: 'Game',
  props: {
    msg: String
  },
  data() {
    return{
      plays:["", "","", "","", "","", "",""],
      resultText:''
    }
  },
  methods:{
    //enters the players move, then runs checks
    onButtonClick(index){
      this.plays.splice(index, 1, 'X')
      if(!this.checkForWin()){
        if(!this.checkForTie()){
          this.opponentMove()
           if(!this.checkForWin()){
             this.checkForTie()
           }
        }
      }
    },
    //check if player or computer won
    checkForWin(){
      //check horizontal win
      if(this.plays[0] === this.plays[1] && this.plays[0] === this.plays[2] && this.plays[0] != ''){
        if(this.plays[0] === 'X'){
          this.resultText = "You Win!"
        }
        else{
          this.resultText = "You Lose!"
        }
        return true
      }
      if(this.plays[3] === this.plays[4] && this.plays[3] === this.plays[5] && this.plays[3] != ''){
        if(this.plays[3] === 'X'){
          this.resultText = "You Win!"
        }
        else{
          this.resultText = "You Lose!"
        }
        return true
      }
      if(this.plays[6] === this.plays[7] && this.plays[6] === this.plays[8] && this.plays[6] != ''){
        if(this.plays[6] === 'X'){
          this.resultText = "You Win!"
        }
        else{
          this.resultText = "You Lose!"
        }
        return true
      }

      //check vertical win
      if(this.plays[0] === this.plays[3] && this.plays[0] === this.plays[6] && this.plays[0] != ''){
        if(this.plays[0] === 'X'){
          this.resultText = "You Win!"
        }
        else{
          this.resultText = "You Lose!"
        }
        return true
      }
      if(this.plays[1] === this.plays[4] && this.plays[1] === this.plays[7] && this.plays[1] != ''){
        if(this.plays[1] === 'X'){
          this.resultText = "You Win!"
        }
        else{
          this.resultText = "You Lose!"
        }
        return true
      }
      if(this.plays[2] === this.plays[5] && this.plays[2] === this.plays[8] && this.plays[2] != ''){
        if(this.plays[2] === 'X'){
          this.resultText = "You Win!"
        }
        else{
          this.resultText = "You Lose!"
        }
        return true
      }

      //check diagonal win
      if(this.plays[0] === this.plays[4] && this.plays[0] === this.plays[8] && this.plays[0] != ''){
        if(this.plays[0] === 'X'){
          this.resultText = "You Win!"
        }
        else{
          this.resultText = "You Lose!"
        }
        return true
      }
      if(this.plays[2] === this.plays[4] && this.plays[2] === this.plays[6] && this.plays[2] != ''){
        if(this.plays[2] === 'X'){
          this.resultText = "You Win!"
        }
        else{
          this.resultText = "You Lose!"
        }
        return true
      }
      return false;
    },
    //check if board is full and game ends in a tie
    checkForTie(){
      let emptySpace = this.plays.findIndex(val => val === '');
      if(emptySpace < 0){
        this.resultText = "Tie Game!"
        return true
      }
      else{
        return false
      }
    },
    //have opponent play
    //Simple AI: looks for first open space and takes it
    opponentMove(){
      let moveIndex = this.plays.findIndex((val => val === ''));
      this.plays.splice(moveIndex, 1, 'O')
    },
    //set the board to empty to play again
    resetBoard(){
      this.plays = ['','','','','','','','','',].slice(0, this.plays.length);
      this.resultText = '';
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
