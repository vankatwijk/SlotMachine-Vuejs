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

/* .SlotMachine-button.is-spin {
  background: rgba(0, 255, 0, .4);
  border: 1px solid rgba(0, 255, 0, .4);
}
.SlotMachine-button.is-spin:hover {
  background: rgba(0, 255, 0, .43);
}
.SlotMachine-button.is-spin:active {
  background: rgba(0, 255, 0, .46);
} */

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
  /* width: 90px;
  height: 209.97px; */
  height: 60vh;
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
  /* top: -119.97px; */
  top: -130px;
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
  /* width: 90px;
  width: 90px; */
  margin: 0 auto;
  text-align: center;
  width: 100%;
    max-width: 200px!important;
    margin: 0 auto;
    align-items: center;
    text-align: center;
}


  /* Davide */
  body {
    background: url("/img/ui/Background.png");
    background-repeat: no-repeat;
    background-size: cover;
    background-attachment: fixed;
  }

  .ma-2 {
    margin: 1rem
  }

  .row {
    margin-bottom: 0
  }

  .logo {
    position: absolute;
    width: 100%;
    top: 0;
    left: 0;
    right: 0;
    margin: 0 auto;
      max-width: 420px;
    z-index: 99;
  }
  .col-buttons {
    min-height: 100px!important;
  }

  button:focus {
    background-color: transparent;
  }

  .btn-spin {
    width: 115px;
    height: 130px;
    border: 0;
    padding: 0;
    box-shadow: 0 0 0 0 transparent;
    margin: .5rem;

    background: url("/img/ui/spin_up.png");
    background-color: transparent;
    background-repeat: no-repeat;
    background-size: cover;    

    position: absolute;
    right: 0; 
    bottom: 0;

    z-index: 10;
  }

  .btn-spin:hover {
    background: url("/img/ui/spin_down.png"); 
    background-repeat: no-repeat;
    background-size: cover;   
    z-index: 11;   
  }

  .btn-buy {
    width: 115px;
    height: 60px;
    border: 0;
    padding: 0;
    box-shadow: 0 0 0 0 transparent;
    margin: .5rem;

    background: url("/img/ui/buy_button_up.png");
    background-color: transparent;
    background-repeat: no-repeat;
    background-size: contain; 

    z-index: 15;   
  } 

  .btn-buy:hover {
    width: 115px;
    height: 60px;
    border: 0;
    padding: 0;
    box-shadow: 0 0 0 0 transparent;
    margin: .5rem;

    background: url("/img/ui/buy_button_down.png");
    background-color: transparent;
    background-repeat: no-repeat;
    background-size: contain;    
  } 

  .toolbar-container {
    max-height: 90px;
    margin: 3rem 0 0 0;
    padding: 0;
    position: relative;
    overflow: visible;
    border-radius: 25px;
    border: 2px solid #2f3e59;
    box-shadow: 0px 2px 13px 1px #668c96;
    background: rgb(2,0,36);
    background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(35,49,74,1) 65%, rgb(219 248 255) 100%);
  }

  .btn-is-win.is-win,
  .btn-is-win.is-win:hover,
  .btn-is-win.is-win.has-win {
    width: 100px;
    height: 100px;
    border: 0;
    padding: 0;
    box-shadow: 0 0 0 0 transparent;
    margin: .5rem;

    background: url("/img/ui/page_inactive.png"), transparent;
    background-color: transparent;
    background-repeat: no-repeat;
    background-size: contain; 
    font-size: 0; 
    position: absolute;
    left: 0; 
    bottom: 0;
  }

  .btn-is-win.has-win,
  .btn-is-win.is-win.has-win {
    background: url("/img/ui/page_active.png"), transparent; 
    background-repeat: no-repeat;
    background-size: contain; 
    font-size: 18px;  
    color: #ffa500;
    padding-top: 5rem;
    text-shadow: 2px 2px 21px #ee6e73;
    text-align: center;     
  }

  .SlotMachine-reels {
    background: rgba(0,0,0,0.5);
    border: 2px solid rgba(0,0,0,0.3);
    border-radius: 15px;  }

  .SlotMachine-payline.col-payline {
      position: absolute;
      top: 50%;
      height: 2px;
      width: 100%;
      background: #fba000;
  }

  .col.col-right {
    background: transparent;
    position: relative;
  }

  .col.col-left {
    background: transparent;
    position: relative;
  }  


  .area-credits {
    width: 115px;
    height: 60px;
    border: 0;
    padding: 0;
    box-shadow: 0 0 0 0 transparent;
    margin: 1.5rem auto 0 auto;

    background: url("/img/ui/credit.png");
    background-color: transparent;
    background-repeat: no-repeat;
    background-size: contain;    
  } 

   .area-credits .area-title {
     display: none;
   }

  .area-credits .area-value {
    padding: 1rem 0 0 0;
    background: transparent;
    border-radius: 0;
    border: 0px solid transparent;
    font-size: 18px;
    text-align: center;
    color: #9e9e9e;
    text-shadow: 0 0 4px rgb(231 149 0 / 50%);
    line-height: 1.5;
  }

  .area-win {
    width: auto;
    height: auto;
    border: 0;
    padding: 0;
    box-shadow: 0 0 0 0 transparent;
    margin: .5rem auto;
    background: url(/img/ui/lines_button_up.png);
    background-color: transparent;
    background-repeat: no-repeat;
    background-size: contain;
    padding-top: 1.7rem;
    min-width: 100px;
  }

   .area-win .area-title {
    text-align: center;
    color: #9e9e9e;
    line-height: .5;
   }

  .area-win .area-value {
    padding: .75rem;
    background: transparent;
    border-radius: 0;
    border: 0px solid transparent;
    font-size: 16px;
    text-align: center;
    color: #9e9e9e;
    text-shadow: 0 0 4px rgb(231 149 0 / 50%);
    line-height: 1.5;
  }

  .area-credits .area-value-sub {
    color: #9e9e9e;
    text-align: center;
  }

  .area-hero {
    position: absolute;
    top: 25%;
    left: 0;
    max-width: 250px;
    z-index: 0;
    transform: skewX(50deg);
    transform: rotateY(180deg);
  }

  .slot-reels-container {
    margin-top: 3rem;
  }


@media only screen and (max-width: 600px) {
     .area-hero {
    position: absolute;
    top: auto;
    bottom: 10%;
    left: 0;
    max-width: 150px;
  }
 }
</style>
