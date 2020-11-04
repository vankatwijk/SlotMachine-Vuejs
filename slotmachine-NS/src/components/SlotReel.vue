<template>
  <StackLayout class="Reel" v-bind:class="{'is-locked':locked}" v-on:mousedown="lock()">
    <StackLayout class="Reel-inner"> 
      
        <Image 
        class="Reel-image" 
        :src="reelTileData[tile1Index].image" 
        /> 
        
        <Image 
        class="Reel-image"
        :src="reelTileData[tile2Index].image" 
        /> 
        
        <Image 
        class="Reel-image" 
        :src="reelTileData[tile3Index].image" 
        /> 
        
        <Image
        class="Reel-image" 
        :src="reelTileData[tile4Index].image" 
        /> 

        <Image 
        class="Reel-image"
        :src="reelTileData[tile5Index].image" 
        /> 
    </StackLayout>
  </StackLayout>
</template>

<script>
  export default {
    name: 'SlotReel',
    props: ['value', 'canlock'],
    //freesound.org
    data: function data() {
      return {
        momentum: null,
        audio: {
          // spin: new Audio('/sounds/spin.mp3'),
          // spinEnd: new Audio('/sounds/spin_end.mp3'),
          // lock: new Audio('/sounds/lock.mp3')
        },
        reelTileCount: 15,
        reelTileData: null,
        reelSourceData: [{
          name: 'Lemon',
          value: 2,
          image: '~/assets/images/hand.png'
        }, {
          name: 'Melon',
          value: 4,
          image: '~/assets/images/pumpkin.png'
        }, {
          name: 'Grapes',
          value: 10,
          image: '~/assets/images/hat.png'
        }, {
          name: 'Cherry',
          value: 16,
          image: '~/assets/images/pot.png'
        }, {
          name: 'Bar',
          value: 32,
          image: '~/assets/images/wild.png'
        }],
        reelIndex: 2,
        tile1Index: 0,
        tile2Index: 1,
        tile3Index: 2,
        tile4Index: 3,
        tile5Index: 4,
        locked: false
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

      this.reelTileData = shuffle(frs);
    },
    mounted: function mounted() {
      this.$el.addEventListener("transitionend", this.animateEnd);
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
          // this.audio.spin.play();
          this.animate();
        } else {
          this.locked = false;
          this.$emit('stopped', this.reelTileData[this.reelIndex], true);
        }
      },
      animate: function animate() {
        this.$el.classList.add('move');
      },
      animateEnd: function animateEnd() {
        this.$el.classList.remove('move');
        this.reIndex();
        this.momentum = this.momentum - 1;
        if (this.momentum > 0) {
          setTimeout(this.animate, 10);
        } else {
          this.$emit('stopped', this.reelTileData[this.reelIndex]);
          // this.audio.spinEnd.play();
          // this.audio.spin.pause();
          // this.audio.spin.currentTime = 0.3;
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
      },
      lock: function lock() {
        if (this.canlock) {
          this.locked = !this.locked;
          // this.audio.lock.play();
        }
      }
    }




  }
</script>