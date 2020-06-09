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
        this.spaces[x][y].player = this.playerOne ? 0 : 1;
        this.checkGameOver();
        this.switchTurn();
      }
    },
    switchTurn() {
      this.playerOne = !this.playerOne;
    },
    checkGameOver() {
      let allSpacesFilled = this.spaces.every((colspace) => colspace.every((space) => space.filled));
      if (allSpacesFilled) {
        setTimeout(() => {
          alert("Game Over !!");
        }, 500);
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
