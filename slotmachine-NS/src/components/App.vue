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
  background-image: url('res://orangepattern');
  background-repeat: repeat;
  background-size: cover;
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

  background-color: white;
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
  padding: 25 0;
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
  font-size: 12;
  color: white;
}
.SlotMachine-statValue {
  font-size: 25;
  text-align: right;
  color: black;
  text-shadow: 0 0 4px rgba(255, 0, 0, .5);

  background-color: white;
  border-color: red;
  border-width: 6;
  border-radius: 6;
}
.SlotMachine-statSub {
  font-size: 9;
  color: white;
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
  /* #4aaa4e; */
  background-color: #368a3a;
  border-color: #368a3a;
  border-width: 10;
  border-radius: 10;

	color: #FFF;
	text-decoration: none;
	display: block;
	padding: 4px;
	border-radius: 10px;
	margin: 50px auto;
	width: 200;
  font-size: 18;
	text-align: center;
	/*Styles for transition*/
	transition: all .2s ease;
	/*Styles for 3d effect*/
	box-shadow: 0px 9px 0px #065781, 0px 9px 25px rgba(0,0,0,.7);
  elevation:5;


}


.SlotMachine-button.is-win {
  background: rgba(255, 0, 0, .4);
  border: 1px solid rgba(255, 0, 0, .5);
}
.SlotMachine-button.is-win.has-win {
  background: rgba(255, 0, 0, .99);
}
.circleButton{

  border-radius: 80;
  background-color: yellowgreen;
  width: 70;
  height: 70;
  font-size: 14;
  color:white;
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
