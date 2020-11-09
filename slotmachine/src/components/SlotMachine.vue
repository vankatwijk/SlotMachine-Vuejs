<template>
    <div class="SlotMachine">
        <div class="container">
            <div class="logo"><img src="img/ui/logo.png" class="responsive-img img-responsive" /></div>
            <div class="SlotMachine-reels slot-reels-container row">
                <div class="SlotMachine-shadow"></div>
                <div class="SlotMachine-payline col-payline"></div>
                <SlotReel ref="reel1" :canlock="canlock" v-on:stopped="reelStopped"></SlotReel>
                <SlotReel ref="reel2" :canlock="canlock" v-on:stopped="reelStopped"></SlotReel>
                <SlotReel ref="reel3" :canlock="canlock" v-on:stopped="reelStopped"></SlotReel>
            </div>
            <div class="area-hero">
                <img src="img/ui/pers.png" class="responsive-img" />
            </div>
            <div class="row toolbar-container bottom">
                <div class="SlotMachine-stats col col-left col-stats xs8 s7 m7 l8 xl8">
                    <div class="container">
                    <div class="row">
                        <div class="col xs4 s4 m4 l4 xl4">
                            <div class="SlotMachine-coin btn-buy btn-coin ma-2" v-on:mousedown="insertCoin()"></div>
                        </div>
                        <div class="col xs4 s4 m4 l4 xl4 ">
                            <div class="SlotMachine-stat is-credit area-credits ma-2">
                                <div class="SlotMachine-statTitle area-title">Credits</div>
                                <div class="SlotMachine-statValue area-value">{{credits.toFixed(2)}}</div>
                                <div class="SlotMachine-statSub area-value-sub">spend {{spend.toFixed(2)}}</div>
                            </div>
                        </div>
                        <div class="col xs4 s4 m4 l4 xl4">
                            <div class="SlotMachine-stat is-win area-win ma-2">
                                <div class="SlotMachine-statTitle area-title">Won</div>
                                <div class="SlotMachine-statValue area-value">{{win.toFixed(2)}}</div>
                            </div>
                        </div>
                    </div>
                    </div>
                </div>
                <div class="SlotMachine-actions col col-right col-buttons xs4 s5 m5 l4 xl4"> 
                    <div class="SlotMachine-button is-win btn-is-win" v-bind:class="{'has-win':win}" v-on:mousedown="takeWin()">Take Win
                    </div>
                    <button class="SlotMachine-button is-spin btn-spin"
                    v-on:mousedown="spin()"></button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
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
                resultData: false,
                canlock: true,
                waslocked: false,
                audio: {
                    win: new Audio('https://freesound.org/data/previews/387/387232_1474204-lq.mp3'),
                    insertCoin: new Audio('https://freesound.org/data/previews/276/276091_5123851-lq.mp3'),
                    bigwin: new Audio('https://freesound.org/data/previews/270/270319_5123851-lq.mp3')
                }
            };
        },
        beforeMount: function beforeMount() {},
        mounted: function mounted() {
            window.addEventListener('keydown', this.keydown);
        },
        computed: {},
        methods: {
            keydown: function keydown(e) {
                console.log(e.which);
                var key = {
                    one: 49,
                    two: 50,
                    three: 51,
                    space: 32
                };
                if (e.which === key.one) {
                    this.$refs.reel1.lock();
                    e.preventDefault();
                } else if (e.which === key.two) {
                    this.$refs.reel2.lock();
                    e.preventDefault();
                } else if (e.which === key.three) {
                    this.$refs.reel3.lock();
                    e.preventDefault();
                } else if (e.which === key.space) {
                    this.spin();
                    e.preventDefault();
                }
            },
            spin: function spin() {
                if (this.credits > 0 && !this.resultData) {
                    this.resultData = [];
                    this.credits = this.credits - 0.5;
                    this.$refs.reel1.run();
                    this.$refs.reel2.run();
                    this.$refs.reel3.run();
                }
            },
            insertCoin: function insertCoin() {
                this.audio.insertCoin.currentTime = 0;
                this.audio.insertCoin.play();
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
                if (wasLocked) this.waslocked = wasLocked;

                this.resultData.push(resultData);
                if (this.resultData.length === 3) {
                    this.checkWin(this.resultData);
                    if (this.waslocked) {
                        this.waslocked = false;
                        this.canlock = false;
                    } else {
                        this.canlock = true;
                    }
                }
            },

            checkWin: function checkWin() {
                if (this.resultData.length === 3) {
                    // ;-)
                    var v1 = this.resultData[0];
                    var v2 = this.resultData[1];
                    var v3 = this.resultData[2];
                    if (v1.name === v2.name && v2.name === v3.name) {
                        if (v1.value >= 10) {
                            this.audio.bigwin.play();
                        } else {
                            this.audio.win.play();
                        }
                        this.win += v1.value;
                        this.waslocked = true; // prevent lock after an unlocked win
                    } else {
                        var bar1 = v1.name === 'Bar';
                        var bar2 = v2.name === 'Bar';
                        var bar3 = v3.name === 'Bar';
                        if (bar1 && bar2 || bar1 && bar3 || bar2 && bar3) {
                            // this.audio.bigwin.play()
                            // this.win += 16
                            // this.waslocked = true // prevent lock after an unlocked win
                        } else if (bar1 || bar2 || bar3) {
                            // this.audio.win.play()
                            // this.win += 4
                            // this.waslocked = true // prevent lock after an unlocked win
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