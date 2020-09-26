<template>
  <div id="app">
    <Timer v-for="(timer, index) in timers" :key="index" :is="timer"/>
    <AddTimer @click.native="addTimer"/>
  </div>
</template>

<script>
  import Timer from './components/Timer';
  import AddTimer from "./components/AddTimer";

  export default {
    name: 'App',
    data: function () {
      return {
        timers: []
      }
    },
    components: {
      Timer,
      AddTimer
    },
    methods: {
      addTimer () {
        this.timers.push(Timer);
      }
    }
  }
</script>

<style lang="less">
  @import url(styles/styles.less);

  #app {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(225px, max-content));
    grid-gap: 44px;
    justify-content: center;
    padding: initial;
  }
</style>
