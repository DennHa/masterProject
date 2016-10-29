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
      <button type="button" name="button" @click="handelIt">click</button>


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
             {{charachteristic.name}}
             <atomProperty v-model="charachteristic.value" :css="characteristics.css" :type="charachteristic.type" ></atomProperty>
             {{charachteristic.unit}}
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

        nukleolus: true,

        //standard properties
        atomSizeStandard: "10" ,
        atomColorStandard: "#4A90E2",

        //atomHeightStart: "5",
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
            return this.characteristics = [],
            this.characteristics = Object.assign([
              {name:"start width", css: "atomWidthStart",  value: "10", unit:"%", type: "number"},
              {name:"start height", css: "atomHeightStart",  value: "10", unit:"%", type: "number" },
              {name:"final width", css: "atomWidthFinal",  value: "50", unit:"%", type: "number" },
              {name:"final height", css: "atomHeightFinal",  value: "50", unit:"%", type: "number" },
            ])
          }
          else if (this.selectedKind == 'atom__color'){
            return this.characteristics = [],
            this.characteristics = Object.assign([
              {name:"start color", css:"ne",   unit:"", type: "color"},
              {name:"final color", css:"ne",   unit:"", type: "color" }
            ])
          } else {

          }
        },




// properties
        //width
        atomWidthStart: function(){
          for (let word in this.characteristics)
            if(this.characteristics[word].css == "atomWidthStart"){
              return this.atomSizeStandard *  (this.characteristics[word].value / this.atomSizeStandard)
            }
          return this.atomSizeStandard
        },

        atomHeightStart: function(){
          for (let word in this.characteristics)
            if(this.characteristics[word].css == "atomHeightStart"){
              return this.atomSizeStandard *  (this.characteristics[word].value / this.atomSizeStandard)
            }
          return this.atomSizeStandard
        },

        atomWidthFinal: function(){
          for (let word in this.characteristics)
            if(this.characteristics[word].css == "atomWidthFinal"){
              return this.atomSizeStandard *  (this.characteristics[word].value / this.atomSizeStandard)
            }
          return this.atomSizeStandard
        },

        atomHeightFinal: function(){
          for (let word in this.characteristics)
            if(this.characteristics[word].css == "atomHeightFinal"){
              return this.atomSizeStandard *  (this.characteristics[word].value / this.atomSizeStandard)
            }
          return this.atomSizeStandard
        },


        //color

    },

    methods: {
      handelIt: function(){
        this.atomStartColor =  this.characteristics[0].value
      },
      //before animation
      beforeEnter: function (el) {
        //el.style.backgroundColor = this.atomStartColor,
        el.style.width = this.atomWidthStart + "%",
        el.style.height = this.atomHeightStart + "%"
        },

      //animation enter
      enter: function (el, done) {
        var vm = this


        Velocity(el,
          {
            width: this.atomWidthFinal + "%",
            height: this.atomHeightFinal + "%"
           //translateX: "200px"
          },
          {
            delay: "2000",
            easing: this.selectedEaseing,
            duration: this.atomDuration,
            complete: function () {
              done()
              if (!vm.stop) vm.nukleolus = false
            }
          }
        )
      },

      //animation leave - just for restart
      leave: function (el, done) {
        var vm = this
        Velocity(el,
          {
            backgroundColor: '#ffffff',
          },
          {
            duration: 1,
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
