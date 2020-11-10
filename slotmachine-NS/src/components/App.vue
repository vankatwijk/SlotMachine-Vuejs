<template>

    <Page>
        <ActionBar title="Slooots" backgroundColor="orangered"/>
        <GridLayout columns="*" rows="*">
            <SlotMachine />
        </GridLayout>
    </Page>

</template>

<script>
import SlotMachine from './SlotMachine.vue'

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
}
.background{
  background-color: orangered;
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
}
.reelContainer{
  border-color: red;
  border-width: 10;
  border-radius: 10;
}

.SlotMachine-payline {
  position: absolute;
  top: 104.994px;
  height: 1px;
  width: 100%;
  background: rgba(0, 0, 0, 0.3);
}


.SlotMachine-stats {
  padding: 10px 0;
}
.SlotMachine-coin {
  width: 6;
  height: 100;
  background: gray;
  border: 3px solid rgb(40, 40, 40);
  border-radius: 6px;
  margin: 12px 10px 0 10px;
}
.SlotMachine-stat {
  margin-right: 10px;
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
  border-radius: 0 0 4px 4px;
}
.SlotMachine-button {
  font-size: 17px;
  font-weight: bold;
  padding: 14px 12px;
  margin-left: 20px;
  border-radius: 5px;
}
.SlotMachine-button:focus {
  outline: none;
}
.SlotMachine-button:active {
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
}
.Reel.is-locked {
/*   opacity: 0.8; */
  background: rgba(0, 0, 0, .1);
}
.Reel:not(:last-child) {
  border-right: 1px solid rgba(0, 0, 0, 0.1);
}
.Reel-inner {
}
.move{
  transition: margin-top 1.00s linear;
  margin-top: 100;
}
.Reel-image {
  width: 90;
  width: 90;
}
</style>
