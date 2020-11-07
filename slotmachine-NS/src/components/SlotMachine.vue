<template>

    <GridLayout columns="*" rows="4*, 2*, 2*" backgroundColor="#3c495e" class="SlotMachine">


        <GridLayout columns="*,auto,auto,auto,*" rows="*,auto,*" row="0" col="1" class="SlotMachine-reels" backgroundColor="yellow">
            <SlotReel col="1" row="1" :spinReel="spinReel" @stopped="reelStopped"></SlotReel>
            <SlotReel col="2" row="1" :spinReel="spinReel" @stopped="reelStopped"></SlotReel>
            <SlotReel col="3" row="1" :spinReel="spinReel" @stopped="reelStopped"></SlotReel>
        </GridLayout>

        <StackLayout orientation="horizontal" row="1" col="0" class="SlotMachine-stats">
            <button class="SlotMachine-coin" width="30" v-on:tap="insertCoin()"></button>
            <StackLayout width="100" class="SlotMachine-stat is-credit">
                <Label class="SlotMachine-statTitle" text="Credits"/>
                <TextField class="SlotMachine-statValue" isEnabled="false" :text="credits.toFixed(2)"/>
                <Label class="SlotMachine-statSub" :text="'spend '+spend.toFixed(2)"/>
            </StackLayout>
            <StackLayout width="100" class="SlotMachine-stat is-win">
                <Label class="SlotMachine-statTitle" text="Won"/>
                <TextField class="SlotMachine-statValue" isEnabled="false" :text="win.toFixed(2)"/>
            </StackLayout>
        </StackLayout>
        <StackLayout orientation="horizontal" row="2" col="0" class="SlotMachine-actions"> 
            <button class="SlotMachine-button is-spin" width="70" @tap="spin()">Play</button>
            <button class="SlotMachine-button is-win" width="70" :class="{'has-win':win}" :tap="takeWin()">Take Win </button>
        </StackLayout>



    </GridLayout>

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
                resultData: [],
                canlock: true,
                waslocked: false,
                audio: {
                    // win: new Audio('https://freesound.org/data/previews/387/387232_1474204-lq.mp3'),
                    // insertCoin: new Audio('https://freesound.org/data/previews/276/276091_5123851-lq.mp3'),
                    // bigwin: new Audio('https://freesound.org/data/previews/270/270319_5123851-lq.mp3')
                },
                spinReel:false
            };
        },
        beforeMount: function beforeMount() {},
        mounted: function mounted() {
            // window.addEventListener('keydown', this.keydown);
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
            spin: function spin() {
                    console.log('spin',this.spinReel);
                if (this.spinReel) {
                    console.log('ifspin',this.spinReel);
                    this.resultData = [];
                    this.credits = this.credits - 0.5;
                    // console.log('----+_+_+_+_+_+_+_++_+_+_+-----')
                    // console.log(this.$refs)
                    // this.$refs.reel1.nativeView.run();
                    // this.$refs.reel2.nativeView.run();
                    // this.$refs.reel3.nativeView.run();
                }
                    console.log('spinReel',this.spinReel);
                    this.spinReel = !this.spinReel;
            },
            insertCoin: function insertCoin() {
                // this.audio.insertCoin.currentTime = 0;
                // this.audio.insertCoin.play();
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
                this.spinReel=false;
                if (wasLocked) this.waslocked = wasLocked;

                var temparray = [];
                temparray.push(resultData);
                if (this.resultData.length === 3) {
                    this.checkWin(this.resultData);
                    if (this.waslocked) {
                        this.waslocked = false;
                        this.canlock = false;
                    } else {
                        this.canlock = true;
                    }
                }

                this.resultData = temparray;
            },

            checkWin: function checkWin() {
                if (this.resultData.length === 3) {
                    // ;-)
                    var v1 = this.resultData[0];
                    var v2 = this.resultData[1];
                    var v3 = this.resultData[2];
                    if (v1.name === v2.name && v2.name === v3.name) {
                        if (v1.value >= 10) {
                            // this.audio.bigwin.play();
                        } else {
                            // this.audio.win.play();
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