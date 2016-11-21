<template name="atomrotation">
<div class="atom__shell">
    <div class="atom__viewer">
        <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave"  v-bind:css="false">
            <div class="atom__nukleolus" v-if="nukleolus"></div>
        </transition>
    </div>

    <div class="atom__properties">
      <h3>rotation</h3>
      <form class="" action="index.html" method="post">
        <input name="name" value="" v-model="value[id].name" class="atom__name">
      </form>

        <div class="atom__timing">
            <h3>timing</h3>
            <form>
                <input name="time" v-model="value[id].timing" value="" type="number">
                <select v-model="value[id].spacing" class="atom__kind">
                   <option v-for="ease in easings" v-bind:value="ease.easeFunction"  >
                     {{ ease.easeFunction }}
                   </option>
              </select>
            </form>
        </div>

        <div class="atom__characteristics">

            <h3>animation</h3>
            <form>
              rotationX(°) <input name="width" v-model="value[id].rotationxstart" type="number"> --> <input name="width" v-model="value[id].rotationxfinal" type="number">
            </form>
            <form>
              rotationY(°) <input name="width" v-model="value[id].rotationystart" type="number"> --> <input name="width" v-model="value[id].rotationyfinal" type="number">
            </form>
            <form>
              rotationZ(°) <input name="width" v-model="value[id].rotationzstart" type="number"> --> <input name="width" v-model="value[id].rotationzfinal" type="number">
            </form>
        </div>
        <div class="subMenu">
          <transition name="fade">
            <div class="subMenu__copied" v-show="copied">copied</div>
          </transition>
          <div v-bind:id="value[id].atomscaleid + value[id].name" v-on:click="copyThis" v-bind:data-clipboard-target="'.' + copyThisValue"></div>

        </div>

        <div v-bind:class="copyThisValue" class="copy">
          //css Animation Specs - {{value[id].name}}  <br>
          .{{value[id].name}} { <br>
          &nbsp;  &nbsp;  animation: {{value[id].name}}_animation {{this.atomDuration}}ms {{this.spacing}};<br>
          &nbsp;  }<br>
          &nbsp;  <br>
          &nbsp;  @keyframes {{value[id].name}}_animation {<br>
          &nbsp;  &nbsp;  0% {<br>
          &nbsp;  &nbsp;  transform: rotatX(){{value[id].rotationxstart}});<br>
          &nbsp;  &nbsp;  transform: rotatY(){{value[id].rotationystart}});<br>
          &nbsp;  &nbsp;  transform: rotatZ(){{value[id].rotationzstart}});<br>
          &nbsp;  }<br>
          &nbsp;  100% {<br>
          &nbsp;  &nbsp;  transform: rotatX(){{value[id].rotationxfinal}});<br>
          &nbsp;  &nbsp;  transform: rotatY(){{value[id].rotationyfinal}});<br>
          &nbsp; &nbsp;  transform: rotatZ(){{value[id].rotationzfinal}});<br>
          &nbsp;  }<br>
          }
        </div>

</div>
</template>

<script>
export default {
    name: "atomrotation",
    props: ['value', 'atomscaleid', 'globalDelay'],
    data() {
        return {
            nukleolus: true,
            copied: false,
            //standard properties
            atomscaleStandard: "50",
            atomColorStandard: "#4A90E2",
            color: "",
            //atomHeightStart: "5",
            //kind
            selectedKind: "atom__scale",
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
            }, ],

            randomElements: ['Hydrogen', 'Helium', 'Lithium', 'Beryllium', 'Boron', 'Carbon', 'Nitrogen', 'Oxygen', 'Fluorine', 'Neon', 'Sodium', 'Magnesium'],
        }
    },
    mounted: function() {
      this.nukleolus = false

    },
    computed: {
        id(){
          return this.atomscaleid
        },
        copyThisValue(){
          return this.value[this.id].atomscaleid + this.value[this.id].name + "_id"
        },
        atomDuration(){
          return this.value[this.atomscaleid].timing
        },
        spacing(){
          return  this.value[this.atomscaleid].spacing
        },
        // properties
        //width
        atomRotationXStart: function() {
            return this.value[this.atomscaleid].rotationxstart

        },

        atomRotationXFinal: function() {
            return this.value[this.atomscaleid].rotationxfinal
        },

        atomRotationYStart: function() {
            return this.value[this.atomscaleid].rotationystart
        },

        atomRotationYFinal: function() {
            return this.value[this.atomscaleid].rotationyfinal
        },
        atomRotationZStart: function() {
            return this.value[this.atomscaleid].rotationzstart
        },

        atomRotationZFinal: function() {
            return this.value[this.atomscaleid].rotationzfinal
        }
    },


    methods: {
      copyThis(){
          var clipboard = new Clipboard('#' + this.value[this.id].atomscaleid + this.value[this.id].name)
          this.copied = true
          var self = this
            setTimeout(function(){
                self.copied = false;
            }, 1000);
        },

        //before animation
        beforeEnter: function(el) {
            el.style.width = this.atomscaleStandard + "px",
            el.style.height = this.atomscaleStandard + "px",
            el.style.transform = "rotateX("+ +this.atomRotationXStart +"deg)",
            el.style.transform = "rotateY("+ +this.atomRotationYStart +"deg)",
            el.style.transform = "rotateZ("+ +this.atomRotationZStart +"deg)",
            Velocity(el, {
                rotateX: this.atomRotationXStart,
                rotateY: this.atomRotationYStart,
                rotateZ: this.atomRotationZStart
            }, {
                duration: 0,
                delay: "0",
                queue: false

            })
        },

        //animation enter
        enter: function(el, done) {
            var vm = this


            Velocity(el, {
                rotateX: this.atomRotationXFinal,
                rotateY: this.atomRotationYFinal,
                rotateZ: this.atomRotationZFinal
            }, {
                delay: this.globalDelay,
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
                duration: 1,
                delay: this.globalDelay,
                complete: function() {
                    done()
                    vm.nukleolus = true
                }
            })
        }
    },

}
</script>
