<template>
  <div id="app">
    <h1>Welcome to connect4</h1>
    <div class="wrapper">
      <div v-bind:key="index" v-for="(colspace, index) in spaces">
        <Colspaces v-bind:colspaces="spaces[index]" v-bind:id="index" v-on:fill-space="fillSpace"/>
      </div>
    </div>
  </div>
</template>

<script>
  import Colspaces from './components/Colspaces';

export default {
  name: 'App',
  components: {
    Colspaces
  },
  data() {
    return {
      playerOne: true,
      spaces: [
        [
          {
            pos: 11,
            player: null,
            filled: false
          },
          {
            pos: 12,
            player: null,
            filled: false
          },
          {
            pos: 13,
            player: null,
            filled: false
          },
          {
            pos: 14,
            player: null,
            filled: false
          }
        ],
        [
          {
            pos: 21,
            player: null,
            filled: false
          },
          {
            pos: 22,
            player: null,
            filled: false
          },
          {
            pos: 23,
            player: null,
            filled: false
          },
          {
            pos: 24,
            player: null,
            filled: false
          }
        ],
        [
          {
            pos: 31,
            player: null,
            filled: false
          },
          {
            pos: 32,
            player: null,
            filled: false
          },
          {
            pos: 33,
            player: null,
            filled: false
          },
          {
            pos: 34,
            player: null,
            filled: false
          }
        ],
        [
          {
            pos: 41,
            player: null,
            filled: false
          },
          {
            pos: 42,
            player: null,
            filled: false
          },
          {
            pos: 43,
            player: null,
            filled: false
          },
          {
            pos: 44,
            player: null,
            filled: false
          }
        ],
        [
          {
            pos: 51,
            player: null,
            filled: false
          },
          {
            pos: 52,
            player: null,
            filled: false
          },
          {
            pos: 53,
            player: null,
            filled: false
          },
          {
            pos: 54,
            player: null,
            filled: false
          }
        ]
      ]
    }
  },
  methods: {
    fillSpace(x,y) {
      if (y > -1) {
        this.spaces[x][y].filled = true;
        this.spaces[x][y].player = this.getActivePlayer();
        this.checkGameOver(x,y);
        this.switchTurn();
      }
    },
    switchTurn() {
      this.playerOne = !this.playerOne;
    },
    getActivePlayer() {
      return this.playerOne ? 0 : 1;
    },
    getActivePlayerColor() {
      return this.playerOne ? 'Green' : 'Red';
    },
    checkVerticalWin(x,y) {
      let vCountUp=0 ;
      let vCountDown=0;
      for (let i=0; this.spaces[x][y+i]!== undefined; i++) {
        if (this.spaces[x][y+i].filled && this.spaces[x][y+i].player === this.getActivePlayer()) {
          vCountUp++;
        } else {
          break;
        }
      }

      for (let i=0; this.spaces[x][y-i]!== undefined; i++) {
        if (this.spaces[x][y-i].filled && this.spaces[x][y-i].player === this.getActivePlayer()) {
          vCountDown++;
        } else {
          break;
        }
      }

      if (vCountUp + vCountDown - 1 >= 4) {
        return true;
      }
      return false;
    },
    checkHorizontalWin(x,y) {
      let hCountRight=0;
      let hCountLeft=0;
      for (let i=0; this.spaces[x+i]!== undefined;i++) {
        if (this.spaces[x+i][y].filled && this.spaces[x+i][y].player === this.getActivePlayer()) {
          hCountRight++;
        } else {
          break;
        }
      }

      for (let i=0; this.spaces[x-i]!== undefined;i++) {
        if (this.spaces[x-i][y].filled && this.spaces[x-i][y].player === this.getActivePlayer()) {
          hCountLeft++;
        } else {
          break;
        }
      }

      if (hCountLeft + hCountRight - 1 >= 4) {
        return true;
      }
      return false;
    },
    checkDiagonalWin(x,y) {
      let diagonalOneCount=0;
      let diagonalTwoCount=0;
      //diagonal1 check
      for (let i=0; this.spaces[x+i]!== undefined && this.spaces[x+i][y+i]!== undefined ; i++) {
        if (this.spaces[x+i][y+i].filled && this.spaces[x+i][y+i].player === this.getActivePlayer()) {
          diagonalOneCount++;
        } else {
          break;
        }
      }
      for (let i=0; this.spaces[x-i]!== undefined && this.spaces[x-i][y-i]!== undefined; i++) {
        if (this.spaces[x-i][y-i].filled && this.spaces[x-i][y-i].player === this.getActivePlayer()) {
          diagonalOneCount++;
        } else {
          break;
        }
      }
      //diagonal2 check
      for (let i=0; this.spaces[x+i]!== undefined && this.spaces[x+i][y-i]!== undefined; i++) {
        if (this.spaces[x+i][y-i].filled && this.spaces[x+i][y-i].player === this.getActivePlayer()) {
          diagonalTwoCount++;
        } else {
          break;
        }
      }
      for (let i=0; this.spaces[x-i]!== undefined && this.spaces[x-i][y+i]!== undefined; i++) {
        if (this.spaces[x-i][y+i].filled && this.spaces[x-i][y+i].player === this.getActivePlayer()) {
          diagonalTwoCount++;
        } else {
          break;
        }
      }

      if (diagonalOneCount-1>=4 || diagonalTwoCount-1>=4) {
        return true;
      }
      return false;
    },
    checkGameOver(x,y) {

      if (this.checkVerticalWin(x,y) || this.checkHorizontalWin(x,y) || this.checkDiagonalWin(x,y)) {
          alert(`Player ${this.getActivePlayerColor()} Won !!`);
      }

      let allSpacesFilled = this.spaces.every((colspace) => colspace.every((space) => space.filled));
      if (allSpacesFilled) {
          alert("Game Over !!");
      }
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  background-color: blanchedalmond;
}

body {
  font-family: Arial, Helvetica, sans-serif;
}

h1 {
  margin: 2%;
  text-align: center;
}

.wrapper {
  display: flex;
  flex-direction: row;
  justify-content: center;
}
</style>
