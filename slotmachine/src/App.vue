<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <SlotMachine />
  </div>
</template>

<script>
import SlotMachine from './components/SlotMachine.vue'

export default {
  name: 'App',
  components: {
    SlotMachine
  }
}
</script>

<style>
html, body {
  margin: 0;
  font-family: sans-serif;
  cursor: default;
}
#app {
  width: 100vw;
  height: 100vh;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: center;
      -ms-flex-pack: center;
          justify-content: center;
  -webkit-box-align: center;
      -ms-flex-align: center;
          align-items: center;
}
.SlotMachine {
  border-radius: 5px;
}
.SlotMachine-reels {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  position: relative;
}
.SlotMachine-shadow {
  border-radius: 4px 4px 0 0;
  pointer-events: none;
  z-index: 99;
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-box-shadow: 
    inset 0 25px 30px -5px rgba(0, 0, 0, 0.1),
    inset 0 5px 10px -2px rgba(0, 0, 0, 0.2),
    inset 0 -25px 30px -5px rgba(0, 0, 0, 0.1),
    inset 0 -5px 10px -2px rgba(0, 0, 0, 0.2);
          box-shadow: 
    inset 0 25px 30px -5px rgba(0, 0, 0, 0.1),
    inset 0 5px 10px -2px rgba(0, 0, 0, 0.2),
    inset 0 -25px 30px -5px rgba(0, 0, 0, 0.1),
    inset 0 -5px 10px -2px rgba(0, 0, 0, 0.2);
}
.SlotMachine-payline {
  position: absolute;
  top: 104.994px;
  height: 1px;
  width: 100%;
  background: rgba(0, 0, 0, 0.3);
}


.SlotMachine-stats {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  background: #000;
  -webkit-box-pack: end;
      -ms-flex-pack: end;
          justify-content: flex-end;
  padding: 10px 0;
}
.SlotMachine-coin {
  width: 6px;
  height: 38px;
  background: grey;
  border: 3px solid rgb(40, 40, 40);
  border-radius: 6px;
  margin: 12px 10px 0 10px;
}
.SlotMachine-coin:hover {
  background: rgb(140, 140, 140);
}
.SlotMachine-stat {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
  margin-right: 10px;
  -webkit-box-flex: 1;
      -ms-flex-positive: 1;
          flex-grow: 1;
}
.SlotMachine-statTitle {
  font-size: 12px;
  color: rgb(60, 60, 60);
}
.SlotMachine-statValue {
  padding: 5px 10px;
  background: rgba(255, 0, 0, .15);
  border-radius: 2px;
  border: 1px solid rgb(0, 0, 0);
  font-size: 25px;
  text-align: right;
  color: rgba(255, 0, 0, .8);
  text-shadow: 0 0 4px rgba(255, 0, 0, .5);
}
.SlotMachine-statSub {
  font-size: 9px;
  color: rgb(50, 50, 50);
  text-align: right;
}



.SlotMachine-actions {
  padding: 20px 10px;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-pack: end;
      -ms-flex-pack: end;
          justify-content: flex-end;
  background: rgb(20, 20, 20);
  border-radius: 0 0 4px 4px;
}
.SlotMachine-button {
  font-size: 17px;
  font-weight: bold;
  padding: 14px 12px;
  margin-left: 20px;
  border-radius: 5px;
  -webkit-box-shadow: 0 1px 2px 2px rgb(0, 0, 0);
          box-shadow: 0 1px 2px 2px rgb(0, 0, 0);
}
.SlotMachine-button:focus {
  outline: none;
}
.SlotMachine-button:active {
  -webkit-box-shadow: 0 0 2px 1px rgb(0, 0, 0);
          box-shadow: 0 0 2px 1px rgb(0, 0, 0);
}

.SlotMachine-button.is-spin {
  background: rgba(0, 255, 0, .4);
  border: 1px solid rgba(0, 255, 0, .4);
}
.SlotMachine-button.is-spin:hover {
  background: rgba(0, 255, 0, .43);
}
.SlotMachine-button.is-spin:active {
  background: rgba(0, 255, 0, .46);
}

.SlotMachine-button.is-win {
  background: rgba(255, 0, 0, .4);
  border: 1px solid rgba(255, 0, 0, .5);
}
.SlotMachine-button.is-win.has-win {
  background: rgba(255, 0, 0, .99);
}
.SlotMachine-button.is-win:hover {
  background: rgba(255, 0, 0, .65);
}
.SlotMachine-button.is-win:active {
  background: rgba(255, 0, 0, .7);
}






.Reel {
  width: 90px;
  height: 209.97px;
  overflow: hidden;
}
.Reel.is-locked {
/*   opacity: 0.8; */
  background: rgba(0, 0, 0, .1);
}
.Reel:not(:last-child) {
  border-right: 1px solid rgba(0, 0, 0, 0.1);
}
.Reel-inner {
  position: relative;
  top: -119.97px;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
      -ms-flex-direction: column;
          flex-direction: column;
}
.Reel.move .Reel-inner{
  -webkit-transition: margin-top 0.04s linear;
  transition: margin-top 0.04s linear;
  margin-top: 90px;
}
.Reel-image {
  width: 90px;
  width: 90px;
}
</style>
