<template>
  <StackLayout ref="reel1" class="Reel" :class="{'is-locked':locked}" @tap="lock()" width="25%" height="200">
    <AbsoluteLayout  height="350" width="100%" :class="animateSpin===true?'Reel-inner move':'Reel-inner '" backgroundColor="white"> 

      <!-- <StackLayout top="100" hight="2" width="100%" backgroundColor="purple">
        <Label text=""></label>
      </StackLayout> -->
      
      <StackLayout top="-140">
        <Image 
        class="Reel-image" 
        :src="'res://'+reelTileData[tile1Index].image" 
        height="70"
        /> 
        
        <Image 
        class="Reel-image"
        :src="'res://'+reelTileData[tile2Index].image" 
        height="70"
        /> 
        
        <Image 
        class="Reel-image" 
        :src="'res://'+reelTileData[tile3Index].image" 
        height="70"
        /> 
        
        <Image
        class="Reel-image" 
        :src="'res://'+reelTileData[tile4Index].image" 
        height="70"
        backgroundColor="green"
        /> 

        <Image 
        class="Reel-image"
        :src="'res://'+reelTileData[tile5Index].image" 
        height="70"
        /> 

      </StackLayout>

    </AbsoluteLayout>
  </StackLayout>
</template>

<script>
  const { TNSPlayer } = require('nativescript-audio');

  export default {
    name: 'SlotReel',
    props: ['value', 'canlock','spinReel'],
    //freesound.org
    data: function data() {
      return {
        momentum: null,

        audioSpin: null,
        audioSpinEnd: null,
        audioLock: null,

        reelTileCount: 15,
        reelTileData: null,
        reelSourceData: [{
          name: 'Lemon',
          value: 2,
          image: 'hand'
        }, {
          name: 'Melon',
          value: 4,
          image: 'pumpkin'
        }, {
          name: 'Grapes',
          value: 10,
          image: 'hat'
        }, {
          name: 'Cherry',
          value: 16,
          image: 'pot'
        }, {
          name: 'Bar',
          value: 32,
          image: 'wild'
        }],
        reelIndex: 2,
        tile1Index: 0,
        tile2Index: 1,
        tile3Index: 2,
        tile4Index: 3,
        tile5Index: 4,
        locked: false,
        animateSpin:false,
      };
    },
    beforeMount: function beforeMount() {
      // Build up the reelTileData array with random tiles  
      var frs = [];


      //var count = this.reelTileCount;
      // this.audio.spin.volume = 0.3;
      // this.audio.spinEnd.volume = 0.8;
      // this.audio.lock.volume = 0.2;
      // this.audio.spin.currentTime = 0.3;
      // Method 1, random until count is reached
      // while (count > 0) {
      //   const fruitIndex = Math.floor(Math.random() * this.reelSourceData.length)
      //   const fruitObject = this.reelSourceData[fruitIndex]
      //   frs.push(fruitObject)
      //   count--
      // }

      // Method 2, sort on value, use index to determine entry count, shuffle
      var reelSourceData = this.reelSourceData.slice(0);
      reelSourceData.sort(function (a, b) {
        return b.value - a.value;
      });
      reelSourceData.forEach(function (sd, i) {
        var times = i + 1 + i; // 0+1+0=1, 3+2+3=8
        while (times > 0) {
          frs.push(sd);
          times--;
        }
      });

      function shuffle(array) {
        var currentIndex = array.length,
          temporaryValue,
          randomIndex;

        // While there remain elements to shuffle...
        while (0 !== currentIndex) {

          // Pick a remaining element...
          randomIndex = Math.floor(Math.random() * currentIndex);
          currentIndex -= 1;

          // And swap it with the current element.
          temporaryValue = array[currentIndex];
          array[currentIndex] = array[randomIndex];
          array[randomIndex] = temporaryValue;
        }

        return array;
      }

      this.reelTileData = frs;
      console.log('[suffle]',this.reelTileData)
    },
    mounted() {

        //sound functionality--------------------------------------
        //spin sounds
          this.audioSpin = new TNSPlayer();
          this.audioSpin.initFromFile({
            audioFile: "~/audio/spin.mp3",
            loop: false,
            autoplay: false
          })
        //spinEnd sounds
          this.audioSpinEnd = new TNSPlayer();
          this.audioSpinEnd.initFromFile({
            audioFile: "~/audio/spin_end.mp3",
            loop: false,
            autoplay: false
          })
        //lock sounds
          this.audioLock = new TNSPlayer();
          this.audioLock.initFromFile({
            audioFile: "~/audio/lock.mp3",
            loop: false,
            autoplay: false
          })


    },
    computed: {},
    methods: {
      run: function run() {
        console.log('run');
        if (!this.locked) {
          var min = 8;
          var max = 28;
          var momentum = Math.floor(Math.random() * (max - min + 1) + min);
          this.momentum = momentum;
          this.audioSpin.play();


          this.animate();
        } else {
          this.locked = false;
          this.$emit('stopped', this.reelTileData[this.reelIndex], true);
        }
      },
      animate: function animate() {
        //this.$el.classList.add('move');
        this.animateSpin = true;
        console.log('animate end')
        setTimeout(() => {
          this.animateEnd()
        }, 10);
      },
      animateEnd: function animateEnd() {
        //this.$el.classList.remove('move');
        this.animateSpin = false;
        this.reIndex();
        this.momentum = this.momentum - 1;
        if (this.momentum > 0) {
          console.log('animate start')

          setTimeout(() => {
            this.animate()
          }, 120);

        } else {
          this.$emit('stopped', this.reelTileData[this.reelIndex]);

          this.audioSpinEnd.play()
          this.audioSpin.pause();
          this.audioSpin.seekTo(0.3);
        }
      },
      reIndex: function reIndex() {
        var end = this.reelTileData.length - 1; //this.reelTileCount - 1
        var index = this.reelIndex === 0 ? end : this.reelIndex - 1;
        // const index = this.index === end ? 0 : this.index + 1
        this.reelIndex = index;
        this.tile1Index = index === 1 ? end : index === 0 ? end - 1 : index - 2;
        this.tile2Index = index === 0 ? end : index - 1;
        this.tile3Index = index;
        this.tile4Index = index === end ? 0 : index + 1;
        this.tile5Index = index === end - 1 ? 0 : index === end ? 1 : index + 2;


        // this.tile5Index = this.tile4Index;
        // this.tile4Index = this.tile3Index;
        // this.tile3Index = this.tile2Index;
        // this.tile2Index = this.tile1Index;
        // this.tile1Index = this.tile5Index;

      },
      lock: function lock() {
        if (this.canlock) {
          this.locked = !this.locked;
          this.audioLock.play();
        }
      }
    },
    watch: {
      spinReel(newVal){
          console.log('inside slotreel',newVal);
        if(newVal){
          this.animateSpin = false;
          this.run();
        }else{
          this.animateSpin = false;
        }
      }
    },




  }
</script>