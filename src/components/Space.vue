<template>
  <div v-bind:style="{'background-color': getActiveColor()}"/>
</template>

<script>
export default {
  name: "Space",
  props: ["space"],
  methods: {
    getActiveColor() {
      if (this.space.filled && this.space.player === 0) {
        return 'green';
      } else if (this.space.filled && this.space.player === 1) {
        return 'red';
      }
      return 'transparent';
    }
  }
}
</script>

<style scoped>
  div {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    border: solid black 2px;
    margin: 10px;
  }
</style>