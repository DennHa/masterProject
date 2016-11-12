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
    </div>

</div>
</template>

<script>
export default {
    name: "atomrotation",
    props: ['value', 'atomsizeid'],
    data() {
        return {
            nukleolus: true,

            //standard properties
            atomSizeStandard: "20",
            atomColorStandard: "#4A90E2",
            color: "",
            //atomHeightStart: "5",
            //kind
            selectedKind: "atom__size",
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
          return this.atomsizeid
        },
        atomDuration(){
          return this.value[this.atomsizeid].timing
        },
        spacing(){
          return  this.value[this.atomsizeid].spacing
        },
        // properties
        //width
        atomRotationXStart: function() {
            return this.value[this.atomsizeid].rotationxstart

        },

        atomRotationXFinal: function() {
            return this.value[this.atomsizeid].rotationxfinal
        },

        atomRotationYStart: function() {
            return this.value[this.atomsizeid].rotationystart
        },

        atomRotationYFinal: function() {
            return this.value[this.atomsizeid].rotationyfinal
        },
        atomRotationZStart: function() {
            return this.value[this.atomsizeid].rotationzstart
        },

        atomRotationZFinal: function() {
            return this.value[this.atomsizeid].rotationzfinal
        }
    },


    methods: {

        clickRemove: function() {

            this.$emit('clickRemove', true)
        },
        //before animation
        beforeEnter: function(el) {
            el.style.width = this.atomSizeStandard + "%",
            el.style.height = this.atomSizeStandard + "%",
            el.style.transform = "rotateX("+ this.atomRotationXStart +"deg)",
            el.style.transform = "rotateY("+ this.atomRotationYStart +"deg)",
            el.style.transform = "rotateZ("+ this.atomRotationZStart +"deg)"//this.atomRotationZStart + "deg"
        },

        //animation enter
        enter: function(el, done) {
            var vm = this


            Velocity(el, {
                rotateX: this.atomRotationXFinal,
                rotateY: this.atomRotationYFinal,
                rotateZ: this.atomRotationZFinal
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
                duration: 1,
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
