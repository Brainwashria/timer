<template>
  <div class="addTimer">
    <button id="add"/>
  </div>
</template>

<script>
  export default {
    name: 'AddTimer'
  }
</script>

<style scoped lang="less">
  .addTimer {
    width: 225px;
    height: 120px;
    background-color: #696969;
    margin-top: 40px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;

    #add {
      background-image: url("../assets/icons/add.svg");
      width: 20px;
      height: 20px;
      background-color: transparent;
    }
  }
</style>
