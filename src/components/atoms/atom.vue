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

      <select v-model="selectedKind" class="atom__kind">
           <option
           v-for="option in options"
           v-bind:value="option.value"
           @click="changeCharacteristics"
           >
             {{ option.text }}
           </option>
      </select>



      <form class="atom__behavior">
        <h3>timing</h3>
        <div v-for="timing in timings">
          <atomProperty v-model="timing.value"  ></atomProperty>
        </div>

        <select v-model="selectedEaseing" class="atom__kind">
             <option v-for="ease in easings" v-bind:value="ease.easeFunction" >
               {{ ease.easeFunction }}
             </option>
        </select>


        <div class="atom__characteristics">
         <h3>characteristics</h3>
           <div v-for="charachteristic in characteristics">
             <atomProperty v-model="charachteristic.value"  ></atomProperty>
           </div>
        </div>
      </form>
      </div>
    </div>

</template>

<script>
import atomProperty from './atom-property.vue'


 export default {
    name: "atom",
    components: {
      atomProperty
    },

    data () {
      return{
        atomName: "",
        atomWidth: "200",
        atomHeight: "200",
        nukleolus: true,

        //kind
        selectedKind: "atom__size",
        options: [
            { text: 'size', value: 'atom__size' },
            { text: 'rotation', value: 'atom__rotation' },
            { text: 'transition', value: 'atom__transition' },
            { text: 'opacity', value: 'atom__opacity' },
            { text: 'color', value: 'atom__color' }
          ],

        //timings
        timings: [
          { kind: 'atomDuration', value: "1000" },
        ],

        //easings
        selectedEaseing: 'easeOutSine',
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
          { easeFunction: 'spring' },
        ],

        characteristics: [
          {hallo: "1"},
          {hallo: "2"}
        ]
      }
    },
    mounted: function () {

      this.nukleolus = false
    },
    computed: {

      //timing
      atomDuration: function(){
        for (var i = 0; i < this.timings.length; i++) {
          if (this.timings[i].kind == "atomDuration"){
            return this.timings[i].value
          }
        }
      },

      //charachteristic
      changeCharacteristics: function(){

        if (this.selectedKind == 'atom__size') {
          for (var i = 0; i  < this.characteristics.length ; i++) {
            this.characteristics.pop()
          }
          this.characteristics.pop() //kill the las entry
          return this.characteristics.push(
            {name: "Joe"}
          )
        }
        else {
          for (var i = 0; i  < this.characteristics.length ; i++) {
            this.characteristics.pop()
          }
          this.characteristics.pop() //kill the las entry
          return this.characteristics.push(
            {name: "Joe"},
            {name: "Joe"}
          )
        }
      }

    },
    methods: {

      //animation
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
            delay:"2000",
            easing: this.selectedEaseing,
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
          { width: this.atomWidth,
            height: this.atomHeight },
          {
            easing: this.selectedEaseing,
            duration: this.atomDuration,
            delay: "2000",
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
