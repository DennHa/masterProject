<template name="atomtranslate">
<div class="atom__shell">
    <div class="atom__viewer">
        <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
            <div class="atom__nukleolus" v-if="nukleolus"></div>
        </transition>
    </div>

    <div class="atom__properties">
      <h3>translate</h3>
      <form class="" action="index.html" method="post">
        <input name="name" value="" v-model="value[id].name" class="atom__name">
      </form>

        <div class="atom__timing">
            <h3>timing</h3>
            <form>
              <input name="time" v-model="value[id].timing" value="" type="number">
              <select v-model="value[id].spacing" class="atom__kind">
                 <option v-for="ease in easings" v-bind:value="ease.easeFunction">
                   {{ ease.easeFunction }}
                 </option>
              </select>
            </form>
        </div>

        <div class="atom__characteristics">

            <h3>animation</h3>
            <form>
              translateX(pt) <input name="width" v-model="value[id].translateXstart" type="number"> --> <input name="width" v-model="value[id].translateXfinal" type="number">
            </form>
            <form>
              translateY(pt) <input name="width" v-model="value[id].translateYstart" type="number"> --> <input name="width" v-model="value[id].translateYfinal" type="number">
            </form>
        </div>
    </div>
    <div class="subMenu">
      <transition name="fade">
        <div class="subMenu__copied" v-show="copied">copied</div>
      </transition>
      <div v-bind:id="value[id].atomtranslateid + value[id].name" v-on:click="copyThis" v-bind:data-clipboard-target="'.' + copyThisValue"></div>

    </div>

    <div v-bind:class="copyThisValue" class="copy">
      //css Animation Specs - {{value[id].name}}  <br>
      .{{value[id].name}} { <br>
      &nbsp;  &nbsp;  animation: {{value[id].name}}_animation {{this.atomDuration}}ms {{this.spacing}};<br>
      &nbsp;  }<br>
      &nbsp;  <br>
      &nbsp;  @keyframes {{value[id].name}}_animation {<br>
      &nbsp;  &nbsp;  0% {<br>
      &nbsp; &nbsp;  transform: translate({{value[id].translateXstart}}px  {{value[id].translateYstart}}px); //in pixel!<br>
      &nbsp;  }<br>
      &nbsp;  100% {<br>
      &nbsp; &nbsp;  transform: translate({{value[id].translateXfinal}}px  {{value[id].translateYfinal}}px); //in pixel!<br>
      &nbsp;  }<br>
      }
    </div>
</div>

</template>

<script>
export default {
    name: "atomtranslate",
    props: ['value', 'atomtranslateid'],
    data() {
        return {
          show: false,
            copied: false,
            nukleolus: true,
            //standard properties
            //atomtranslateStandard: "50",
            atomColorStandard: "#4A90E2",
            color: "",
            //atomtranslateYstart: "5",
            //kind

            selectedEaseing: 'easeOutSine',
            easings: [{
                easeFunction: 'linear'
            }, {
                easeFunction: 'easeInSine'
            }, {
                easeFunction: 'easeOutSine'
            }, {
                easeFunction: 'easeInOutSine'
            }, {
                easeFunction: 'easeInQuad'
            }, {
                easeFunction: 'easeOutQuad'
            }, {
                easeFunction: 'easeInOutQuad'
            }, {
                easeFunction: 'easeInCubic'
            }, {
                easeFunction: 'easeOutCubic'
            }, {
                easeFunction: 'easeInQuart'
            }, {
                easeFunction: 'easeOutQuart'
            }, {
                easeFunction: 'easeInOutQuart'
            }, {
                easeFunction: 'easeInQuint'
            }, {
                easeFunction: 'easeOutQuint'
            }, {
                easeFunction: 'easeInOutQuint'
            }, {
                easeFunction: 'easeInExpo'
            }, {
                easeFunction: 'easeOutExpo'
            }, {
                easeFunction: 'easeInOutExpo'
            }, {
                easeFunction: 'easeInCirc'
            }, {
                easeFunction: 'easeOutCirc'
            }, {
                easeFunction: 'easeInOutCirc'
            }, {
                easeFunction: 'easeInBack'
            }, {
                easeFunction: 'easeOutBack'
            }, {
                easeFunction: 'easeInOutBack'
            }, {
                easeFunction: 'easeInElastic'
            }, {
                easeFunction: 'easeOutElastic'
            }, {
                easeFunction: 'easeInOutElastic'
            }, {
                easeFunction: 'spring'
            }, ]
        }
    },
    mounted: function() {
      this.nukleolus = false


    },
    computed: {

        id(){
          return this.atomtranslateid
        },
        //
        copyThisValue(){
          return this.value[this.id].atomtranslateid + this.value[this.id].name + "_id"
        },
        //
        atomDuration(){
          return this.value[this.atomtranslateid].timing
        },
        spacing(){
          return  this.value[this.atomtranslateid].spacing
        },
        // properties
        //width
        atomtranslateXstart: function() {
            return +this.value[this.atomtranslateid].translateXstart * this.value[this.atomtranslateid].viewPortScaleX - 180 * this.value[this.atomtranslateid].viewPortScaleX

        },

        atomtranslateYstart: function() {
            return +this.value[this.atomtranslateid].translateYstart
            * this.value[this.atomtranslateid].viewPortScaleY - 320 * this.value[this.atomtranslateid].viewPortScaleX
        },

        atomtranslateXfinal: function() {
            return  +this.value[this.atomtranslateid].translateXfinal * this.value[this.atomtranslateid].viewPortScaleX - 180 * this.value[this.atomtranslateid].viewPortScaleX
        },

        atomtranslateYfinal: function() {
            return  +this.value[this.atomtranslateid].translateYfinal * this.value[this.atomtranslateid].viewPortScaleY - 320 * this.value[this.atomtranslateid].viewPortScaleX
        },


    },


    methods: {
        //copyThis
        copyThis(){
          var clipboard = new Clipboard('#' + this.value[this.id].atomtranslateid + this.value[this.id].name)

          this.copied = true
          var self = this
            setTimeout(function(){
                self.copied = false;
            }, 1000);
        },

        //before animation
        beforeEnter: function(el) {
            el.style.opacity = 0, //gegen das flackern
          Velocity(el, {
              opacity: 1,
              translateX: +this.atomtranslateXstart  + "px",
              translateY: +this.atomtranslateYstart  + "px"
          }, {
              delay: 0,

              duration: 0,

          })
        },

        //animation enter
        enter: function(el, done) {
            var vm = this


            Velocity(el, {
                translateX: +this.atomtranslateXfinal + "px",
                translateY: +this.atomtranslateYfinal + "px"
            }, {
                delay: "2000",
                easing: this.spacing,
                duration: this.atomDuration,
                complete: function() {
                    done()
                    if (!vm.stop) vm.nukleolus = false
                }
            })
        },

        //animation leave - just for restart
        leave: function(el, done) {
            var vm = this
            Velocity(el, {
                backgroundColor: '#ffffff',
            }, {
                duration: 0,
                delay: "2000",
                complete: function() {
                    done()
                    vm.nukleolus = true
                }
            })
        }
    },

}
</script>
