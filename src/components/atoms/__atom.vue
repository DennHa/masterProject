<template name="atom">
<div class="atom__shell">
    <div class="atom__remove" v-on:click="clickRemove">x</div>
    <div class="atom__viewer">
        <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
            <div class="atom__nukleolus" v-if="nukleolus"></div>
        </transition>
    </div>

    <div class="atom__properties">
        <atomProperty class="atom__sectionName" v-model="atomName" :nameElement="true" v-bind:acceptType="'all'"></atomProperty>

        <div class="atom__timing">
            <h3>timing</h3>
            <form>
                <div v-for="timing in timings">
                    <atomProperty v-model="timing.value" v-bind:acceptType="timing.type" :unit="timing.unit"></atomProperty>
                </div>
                <form>
                    <select v-model="selectedEaseing" class="atom__kind">
                   <option v-for="ease in easings" v-bind:value="ease.easeFunction" >
                     {{ ease.easeFunction }}
                   </option>
              </select>
        </div>

        <div class="atom__characteristics">

            <h3>animation</h3>
            <select v-model="selectedKind" class="atom__kind">
                <option
                v-for="option in options"
                v-bind:value="option.value"
                v-on:click="changeCharacteristics"
               >
                 {{ option.text }}
                </option>
          </select>
            <form>
                <div v-for="characteristic in characteristics" style="{width:50%}">
                    <atomProperty v-model="characteristic.value" :prefix="characteristic.prefix" :unit="characteristic.unit" :acceptType="characteristic.type" :max="characteristic.max" :min="characteristic.min"></atomProperty>
                </div>
            </form>
        </div>
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
    props: [

    ],
    data() {
        return {
            nukleolus: true,
            atomName: "",
            //standard properties
            atomSizeStandard: "20",
            atomColorStandard: "#4A90E2",
            color: "",
            //atomHeightStart: "5",
            //kind
            selectedKind: "atom__size",
            options: [{
                text: 'size',
                value: 'atom__size'
            }, {
                text: 'rotation',
                value: 'atom__rotation'
            }, {
                text: 'transition',
                value: 'atom__transition'
            }, {
                text: 'opacity',
                value: 'atom__opacity'
            }, {
                text: 'color',
                value: 'atom__color'
            }],

            //timings
            timings: [{
                kind: 'atomDuration',
                value: "1000",
                unit: "ms",
                type: "number"
            }, ],

            //easings
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

            characteristics: [],

            randomElements: ['Hydrogen', 'Helium', 'Lithium', 'Beryllium', 'Boron', 'Carbon', 'Nitrogen', 'Oxygen', 'Fluorine', 'Neon', 'Sodium', 'Magnesium'],
        }
    },
    mounted: function() {
        this.nukleolus = false,
        this.atomName = this.randomElements[Math.floor((Math.random() * 11) + 1)] + "-" + this.randomElements[Math.floor((Math.random() * 11) + 1)] + "ide"
    },
    computed: {
        //timing
        atomDuration: function() {
            for (var i = 0; i < this.timings.length; i++) {
                if (this.timings[i].kind == "atomDuration") {
                    return this.timings[i].value
                }
            }
        },

        //charachteristic
        changeCharacteristics: function() {
            if (this.selectedKind == 'atom__size') {
                return this.characteristics = [],
                    this.characteristics = Object.assign([{
                        prefix: "width from",
                        css: "atomWidthStart",
                        value: "10",
                        unit: "%",
                        type: "number",
                        min: "0",
                        max: "100"
                    }, {
                        prefix: "to",
                        css: "atomWidthFinal",
                        value: "50",
                        unit: "%",
                        type: "number",
                        min: "0",
                        max: "100"
                    }, {
                        prefix: "height from",
                        css: "atomHeightStart",
                        value: "10",
                        unit: "%",
                        type: "number",
                        min: "0",
                        max: "100"
                    }, {
                        prefix: "to",
                        css: "atomHeightFinal",
                        value: "50",
                        unit: "%",
                        type: "number",
                        min: "0",
                        max: "100"
                    }, ])
            } else if (this.selectedKind == 'atom__rotation') {
                return this.characteristics = [],
                    this.characteristics = Object.assign([{
                        prefix: "start rotation",
                        css: "atomRotationStart",
                        value: "0",
                        unit: "°",
                        type: "number"
                    }, {
                        prefix: "to",
                        css: "atomRotationFinal",
                        value: "45",
                        unit: "°",
                        type: "number"
                    }])
            } else if (this.selectedKind == 'atom__transition') {
                return this.characteristics = [],
                    this.characteristics = Object.assign([{
                        prefix: "x-position from",
                        css: "atomXPosStart",
                        value: "10",
                        unit: "%",
                        type: "number",
                        min: "0",
                        max: "100"
                    }, {
                        prefix: "to",
                        css: "atomXPosFinal",
                        value: "50",
                        unit: "%",
                        type: "number",
                        min: "0",
                        max: "100"
                    }, {
                        prefix: "y-position from",
                        css: "atomYPosStart",
                        value: "10",
                        unit: "%",
                        type: "number",
                        min: "0",
                        max: "100"
                    }, {
                        prefix: "to",
                        css: "atomYPosFinal",
                        value: "50",
                        unit: "%",
                        type: "number",
                        min: "0",
                        max: "100"
                    }, ])

            } else if (this.selectedKind == 'atom__opacity') {
                return this.characteristics = [],
                    this.characteristics = Object.assign([{
                        prefix: "from opacity",
                        css: "atomOpacityStart",
                        value: "100",
                        unit: "%",
                        type: "number"

                    }, {
                        prefix: "to",
                        css: "atomOpacityFinal",
                        value: "0",
                        unit: "%",
                        type: "number"
                    }])
            } else if (this.selectedKind == 'atom__color') {
                return this.characteristics = [],
                    this.characteristics = Object.assign([{
                        prefix: "from",
                        css: "atomColorStart",
                        value: "#4A90E2",
                        unit: "",
                        type: "color"

                    }, {
                        prefix: "to",
                        css: "atomColorFinal",
                        value: "#50E3C2",
                        unit: "",
                        type: "color"

                    }])
            }
        },



        // properties
        //width
        atomWidthStart: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomWidthStart") {
                    return this.atomSizeStandard * (this.characteristics[nmr].value / this.atomSizeStandard)
                }
            return this.atomSizeStandard
        },

        atomHeightStart: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomHeightStart") {
                    return this.atomSizeStandard * (this.characteristics[nmr].value / this.atomSizeStandard)
                }
            return this.atomSizeStandard
        },

        atomWidthFinal: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomWidthFinal") {
                    return this.atomSizeStandard * (this.characteristics[nmr].value / this.atomSizeStandard)
                }
            return this.atomSizeStandard
        },

        atomHeightFinal: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomHeightFinal") {
                    return this.atomSizeStandard * (this.characteristics[nmr].value / this.atomSizeStandard)
                }
            return this.atomSizeStandard
        },

        //rotation
        atomRotationStart: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomRotationStart") {
                    return this.characteristics[nmr].value
                }
            return 0
        },
        atomRotationFinal: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomRotationFinal") {
                    return this.characteristics[nmr].value
                }
            return 0
        },


        // transition
        //  let viewPortWidth = this.
        atomXPosStart: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomXPosStart") {
                    return this.characteristics[nmr].value
                }
            return 0
        },

        atomYPostStart: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomYPosStart") {
                    return this.characteristics[nmr].value
                }
            return 0
        },

        atomXPosFinal: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomXPosFinal") {
                    return this.characteristics[nmr].value
                }
            return 0
        },

        atomYPosFinal: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomYPosFinal") {
                    return this.characteristics[nmr].value
                }
            return 0
        },

        //opacity
        atomOpacityStart: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomOpacityStart") {
                    return this.characteristics[nmr].value / "100"
                }
            return 1
        },

        atomOpacityFinal: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomOpacityFinal") {
                    return this.characteristics[nmr].value / "100"
                }
            return 1
        },

        //color
        atomColorStart: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomColorStart") {
                    return this.characteristics[nmr].value
                }
            return "#4A90E2"
        },

        atomColorFinal: function() {
            for (let nmr in this.characteristics)
                if (this.characteristics[nmr].css == "atomColorFinal") {
                    return this.characteristics[nmr].value
                }
            return "#4A90E2"
        }
    },


    methods: {

        clickRemove: function() {

            this.$emit('clickRemove', true)
        },
        //before animation
        beforeEnter: function(el) {
            //el.style.backgroundColor = this.atomStartColor,
            el.style.width = this.atomWidthStart + "%",
            el.style.height = this.atomHeightStart + "%",
            el.style.rotateZ = this.atomRotationStart + "deg",
            el.style.translateX = this.atomXPosStart + "vw",
            el.style.translateY = this.atomYPosStart + "vw",
            el.style.opacity = this.atomOpacityStart,
            el.style.backgroundColor = this.atomColorStart

        },

        //animation enter
        enter: function(el, done) {
            var vm = this


            Velocity(el, {
                width: this.atomWidthFinal + "%",
                height: this.atomHeightFinal + "%",
                rotateZ: this.atomRotationFinal + "deg",
                translateX: this.atomXPosFinal + "vw",
                translateY: this.atomYPosFinal + "vw",
                opacity: this.atomOpacityFinal,
                backgroundColor: this.atomColorFinal
            }, {
                delay: "2000",
                easing: this.selectedEaseing,
                duration: this.atomDuration,
                complete: function() {
                    done()
                    if (!vm.stop) vm.nukleolus = false
                    vm.forceUpdate()
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
