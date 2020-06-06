<template>
  <div>
    <div class="colwrapper">
      <div v-bind:key="space.pos" v-for="space in colspaces">
          <Space v-bind:space="space"/>
      </div>
    </div>
    <button class="btn">Drop</button>
  </div>
</template>

<script>
import Space from './Space'

export default {
  name: "Colspaces",
  components: {
    Space
  },
  props: ["colspaces"]
}
</script>

<style scoped>
.colwrapper {
  margin: 25px;
}
</style>