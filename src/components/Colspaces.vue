<template>
    <div class="colwrapper">
      <button class="btn" v-on:click="$emit('fill-space', id, lastEmptySpace())">Drop</button>
      <div v-bind:key="space.pos" v-for="space in colspaces">
          <Space v-bind:space="space"/>
      </div>
    </div>
</template>

<script>
import Space from './Space'

export default {
  name: "Colspaces",
  components: {
    Space
  },
  props: ["colspaces", "id"],
  methods: {
    lastEmptySpace() {
      for(let i=this.colspaces.length-1; i>=0; i--) {
        if (!this.colspaces[i].filled) {
          return i;
        }
      }
      return -1;
    }
  }
}
</script>

<style scoped>
.colwrapper {
  margin: 25px;
}
.btn {
  width: 100%;
  height: 50px;
}
</style>