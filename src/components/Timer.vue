<template>
  <div class="TimerContainer" v-bind:class="{active : isRunning}">
    <div class="FirstRowOfContainer">
      <span id="hours" v-if="showHours">{{ hours }}:</span>
      <span id="min" v-if="showMinutes">{{ min }}:</span>
      <span id="sec">{{ sec }}</span>
    </div>
    <div class="SecondRowOfContainer">
      <div class="buttonController">
        <button v-if="isRunning" id="pause" @click="stopTimer"/>
        <button v-else id="play" @click="startTimer"/>
        <button id="stop" @click="clearTimer"/>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'Timer',
    data: function () {
      return {
        isRunning: false,
        showMinutes: false,
        showHours: false,
        timer: null,
        sec: '0',
        min: '0',
        hours: '0'
      }
    },
    methods: {
      clearTimer () {
        clearInterval(this.timer);
        this.sec = '0';
        this.min = '0';
        this.hours = '0';
        this.isRunning = false;
        this.showHours = false;
        this.showMinutes = false;
      },
      calculate () {
        this.sec = (parseInt(this.sec) + 1).toString();

        if (parseInt(this.sec) > 59) {
          this.sec = '00';
          this.min = (parseInt(this.min) + 1).toString();
          this.showMinutes = true;
        }
        if (parseInt(this.min) > 59) {
          this.min = '00';
          this.hours = (parseInt(this.hours) + 1).toString();
          this.showHours = true;
        }
        const isItNeedToAddZeroesToMinutes = parseInt(this.hours) > 0 && parseInt(this.min) < 10;
        if (isItNeedToAddZeroesToMinutes) {
          this.min = this.min.padStart(2, '0');
        }
        const isItNeedToAddZeroesToSeconds = (parseInt(this.min) > 0 || parseInt(this.hours) > 0) && parseInt(this.sec) < 10;
        if (isItNeedToAddZeroesToSeconds) {
          this.sec = this.sec.padStart(2, '0');
        }
      },
      startTimer () {
        this.timer = setInterval(() => this.calculate(), 1000);
        this.isRunning = true;
      },
      stopTimer () {
        clearInterval(this.timer);
        this.isRunning = false;
      }
    }
  }
</script>

<style scoped lang='less'>
  .TimerContainer {
    color: #9e9e9e;
    width: 225px;
    height: 120px;
    background-color: #696969;
    margin-top: 40px;
    display: flex;
    flex-direction: column;

    .FirstRowOfContainer {
      height: 50%;
      font-size: 20px;
      display: flex;
      justify-content: center;
      align-items: center;
      border-bottom: 1px solid #9e9e9e;
    }

    .SecondRowOfContainer {
      height: 50%;
      display: flex;
      justify-content: center;
      align-items: center;

      .buttonController {
        width: 40%;
        display: flex;
        justify-content: space-between;

        button {
          background-repeat: no-repeat;
          background-color: transparent;
          cursor: pointer;
          height: 20px;
        }

        #play {
          background-image: url("../assets/icons/play.svg");
          width: 17px;
        }

        #stop {
          background-image: url("../assets/icons/stop.svg");
          width: 20px;
        }

        #pause {
          background-image: url("../assets/icons/activePause.svg");
          width: 10px;
        }
      }
    }
  }

  .active {
    color: white;

    .FirstRowOfContainer {
      border-bottom: 1px solid white;
    }

    .SecondRowOfContainer {
      .buttonController {
        #stop {
          background-image: url("../assets/icons/activeStop.svg");
        }
      }
    }
  }
</style>
