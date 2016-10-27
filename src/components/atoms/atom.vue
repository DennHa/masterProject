easeFunction<template name="atom">
    <div class="atom__shell">
      <form class="atom__name" v-on:submit.prevent>
        <input type="" name="atome_nameChange" v-model="atomName" placeholder="Name"/>
        <input type="text" style="display:none;">
      </form>
      <div class="atom__viewer">
        <transition
          v-on:before-enter="beforeEnter"
          v-on:enter="enter"
          v-on:leave="leave"
          v-bind:css="false"
        >
          <div class="atom__nukleolus" v-if="nukleolus"></div>
         </transition>
      </div>

      <div class="atom__properties">

      <select v-model="selected" class="atom__kind">
           <option v-for="option in options" v-bind:value="option.value" >
             {{ option.text }}
           </option>
      </select>



      <form class="atom__behavior">
        <h3>timing</h3>
        <div v-for="timing in timings">
          <atomTiming v-model="timing.value"></atomTiming>
        </div>


        <div class="atom__characteristics">
         <h3>characteristics</h3>

         <!-- size -->
         <span v-if="selected == 'atom__size'">
           <input type="number"  v-model="atomWidth" />
           <input type="number" v-model="atomHeight">
         </span>

        </div>
      </form>
      </div>
    </div>

</template>

<script>
import atomTiming from './atom-timing.vue'


 export default {
    name: "atom",
    components: {
      atomTiming
    },

    data () {
      return{
        atomName: "",
        atomWidth: "20",
        atomHeight: "20",
        nukleolus: true,
        selected: "atom__size",
        easings: [
          { easeFunction: 'linear' },
          { easeFunction: 'easeInSine' },
          { easeFunction: 'easeOutSine' },
          { easeFunction: 'easeInOutSine' },
          { easeFunction: 'easeInQuad' },
          { easeFunction: 'easeOutQuad' },
          { easeFunction: 'easeInOutQuad' },
          { easeFunction: 'easeInCubic' },
          { easeFunction: 'easeOutCubic' },
          { easeFunction: 'easeInQuart' },
          { easeFunction: 'easeOutQuart' },
          { easeFunction: 'easeInOutQuart' },
          { easeFunction: 'easeInQuint' },
          { easeFunction: 'easeOutQuint' },
          { easeFunction: 'easeInOutQuint' },
          { easeFunction: 'easeInExpo' },
          { easeFunction: 'easeOutExpo' },
          { easeFunction: 'easeInOutExpo' },
          { easeFunction: 'easeInCirc' },
          { easeFunction: 'easeOutCirc' },
          { easeFunction: 'easeInOutCirc' },
          { easeFunction: 'easeInBack' },
          { easeFunction: 'easeOutBack' },
          { easeFunction: 'easeInOutBack' },
          { easeFunction: 'easeInElastic' },
          { easeFunction: 'easeOutElastic' },
          { easeFunction: 'easeInOutElastic' },
          { easeFunction: 'easeInBounce' },
          { easeFunction: 'easeOutBounce' },
          { easeFunction: 'easeInOutBounce' },
        ],
        options: [
            { text: 'size', value: 'atom__size' },
            { text: 'rotation', value: 'atom__rotation' },
            { text: 'transition', value: 'atom__transition' },
            { text: 'opacity', value: 'atom__opacity' },
            { text: 'color', value: 'atom__color' }
          ],
        timings: [
          { kind: 'atomDuration', value: "1000" },
          { kind: 'atomDelay', value: "0" },
        ]
      }
    },
    mounted: function () {
      this.nukleolus = false
    },
    computed: {
      atomDuration: function(){
        for (var i = 0; i < this.timings.length; i++) {
          if (this.timings[i].kind == "atomDuration"){
            return this.timings[i].value
          }
        }
      },

      atomDDelay: function(){
        for (var i = 0; i < this.timings.length; i++) {
          if (this.timings[i].kind == "atomDelay"){
            return this.timings[i].value
          }
        }
      }

    },
    methods: {
      beforeEnter: function (el) {
        el.style.width = '2vw'
        el.style.height = '2vw'
        },
      enter: function (el, done) {
        var vm = this
        Velocity(el,
          { width: this.atomWidth,
           height: this.atomHeight ,
           //translateX: "200px"
          },
          {
           easing: "easeInSine",
            duration: this.atomDuration,
            complete: function () {
              done()
              if (!vm.stop) vm.nukleolus = false
            }
          }
        )
      },
      leave: function (el, done) {
        var vm = this
        Velocity(el,
          { width: '2vw',
            height: '2vw' },
          {
            duration: this.atomDuration,
            complete: function () {
              done()
              vm.nukleolus = true
            }
          }
        )
      }
    },

  }
</script>
