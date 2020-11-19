<template>

    <GridLayout columns="*" rows="4*, 2*, 2*" class="SlotMachine">


        <GridLayout columns="*,auto,*" rows="*,auto,*" row="0" col="1" class="SlotMachine-reels background" >

            <StackLayout orientation="horizontal" col="1" row="1" class="reelContainer">
                <SlotReel :spinReel="spinReel" @stopped="reelStopped"></SlotReel>
                <SlotReel :spinReel="spinReel" @stopped="reelStopped"></SlotReel>
                <SlotReel :spinReel="spinReel" @stopped="reelStopped"></SlotReel>
            </StackLayout>

        </GridLayout>

        <GridLayout columns="*,auto,auto,*" rows="*" row="1" col="0" class="SlotMachine-stats background">

            <button col="0" row="0" class="circleButton" v-on:tap="insertCoin()">Buy</button>

            <StackLayout col="1" row="0" width="100" class="SlotMachine-stat is-credit">
                <Label class="SlotMachine-statTitle" text="Credits"/>
                <Label class="SlotMachine-statValue" :text="credits.toFixed(2)"/>
                <Label class="SlotMachine-statSub" :text="'spend '+spend.toFixed(2)"/>
            </StackLayout>

            <StackLayout col="2" row="0" width="100" class="SlotMachine-stat is-win">
                <Label class="SlotMachine-statTitle" text="Won"/>
                <Label class="SlotMachine-statValue" :text="win.toFixed(2)"/>
            </StackLayout>

            <button col="3" row="0" class="circleButton" :class="{'has-win':win}" @tap="takeWin()">Take</button>

        </GridLayout>

        <GridLayout rows="auto" columns="*" row="2" col="0" class="SlotMachine-actions background"> 
            <button row="0" horizontalAlignment="center" class="SlotMachine-button is-spin" @tap="spin()">Spin</button>
        </GridLayout>



    </GridLayout>

</template>

<script>
    const { TNSPlayer } = require('nativescript-audio');
    import SlotReel from './SlotReel';

    export default {
        name: 'SlotMachine',
        components:{
            SlotReel
        },
        data: function data() {
            return {
                spend: 6,
                credits: 6,
                win: 0,
                resultData: [],
                canlock: true,
                waslocked: false,

                audioWin:null,
                audioInsertCoin:null,
                audioBigWin:null,

                spinReel:false
            };
        },
        beforeMount() {},
        mounted() {

        //sound functionality--------------------------------------
        //spin sounds
          this.audioWin = new TNSPlayer();
          this.audioWin.initFromFile({
            audioFile: "~/audio/win.mp3",
            loop: false,
            autoplay: false
          })
        //spinEnd sounds
          this.audioInsertCoin = new TNSPlayer();
          this.audioInsertCoin.initFromFile({
            audioFile: "~/audio/insert_coin.mp3",
            loop: false,
            autoplay: false
          })
        //lock sounds
          this.audioBigWin = new TNSPlayer();
          this.audioBigWin.initFromFile({
            audioFile: "~/audio/big_win.mp3",
            loop: false,
            autoplay: false
          })

        },
        computed: {},
        methods: {
            // keydown: function keydown(e) {
            //     console.log(e.which);
            //     var key = {
            //         one: 49,
            //         two: 50,
            //         three: 51,
            //         space: 32
            //     };
            //     if (e.which === key.one) {
            //         this.$refs.reel1.lock();
            //         e.preventDefault();
            //     } else if (e.which === key.two) {
            //         this.$refs.reel2.lock();
            //         e.preventDefault();
            //     } else if (e.which === key.three) {
            //         this.$refs.reel3.lock();
            //         e.preventDefault();
            //     } else if (e.which === key.space) {
            //         this.spin();
            //         e.preventDefault();
            //     }
            // },
            spin() {
                console.log('spin',this.spinReel);
                if (!this.spinReel && this.credits > 0) {
                    console.log('ifspin',this.spinReel);
                    this.resultData = [];
                    this.credits = (this.credits - 0.5);
                    console.log('spinReel',this.spinReel);
                    this.spinReel = !this.spinReel;
                }
            },
            insertCoin: function insertCoin() {
                this.audioInsertCoin.seekTo(0);
                this.audioInsertCoin.play();
                this.credits += .5;
                this.spend += .5;
            },
            takeWin: function takeWin() {
                if (this.win > 0) {
                    this.credits += this.win;
                    this.win = 0;
                }
            },
            reelStopped: function reelStopped(resultData, wasLocked) {
                console.log('Result Data',resultData)
                this.spinReel=false;
                if (wasLocked) this.waslocked = wasLocked;

                //var temparray = [];
                this.resultData.push(resultData);

                if (this.resultData.length === 3) {
                    this.checkWin(this.resultData);
                    if (this.waslocked) {
                        this.waslocked = false;
                        this.canlock = false;
                    } else {
                        this.canlock = true;
                    }
                    this.resultData = []
                }

                //this.resultData = temparray;
            },

            checkWin: function checkWin() {
                if (this.resultData.length === 3) {
                    // ;-)
                    var v1 = this.resultData[0];
                    var v2 = this.resultData[1];
                    var v3 = this.resultData[2];
                    if (v1.name === v2.name && v2.name === v3.name) {
                        if (v1.value >= 10) {
                            this.audioBigWin.play();
                        } else {
                            this.audioWin.play();
                        }
                        this.win += v1.value;
                        this.waslocked = true; // prevent lock after an unlocked win
                    } else {
                        var bar1 = v1.name === 'Bar';
                        var bar2 = v2.name === 'Bar';
                        var bar3 = v3.name === 'Bar';
                        if (bar1 && bar2 || bar1 && bar3 || bar2 && bar3) {
                            this.audioBigWin.play()
                            this.win += 16
                            this.waslocked = true // prevent lock after an unlocked win
                        } else if (bar1 || bar2 || bar3) {
                            this.audioWin.play()
                            this.win += 4
                            this.waslocked = true // prevent lock after an unlocked win
                        } else {
                            // Lose : (
                        }
                    }
                }
                this.resultData = false;
            }
        }
    }
</script>