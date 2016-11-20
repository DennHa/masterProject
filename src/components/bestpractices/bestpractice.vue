<template name="bestpractice">
<div class="bestpractice__bond">

    <div class="bestpractice__viewer">
        <!-- <div class="molecule__bestpracticeWrapper">
            <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
                <div class="molecule__nukleolus" v-if="nukleolus"></div>
            </transition>
        </div> -->
        <nukleolus :molecule-collection="moleculeCollection" :atom-collection="atomCollection" :organism-collection="organismCollection" element="0"  v-model="value" :this-delay="value[id].firstElementDelay">
        </nukleolus>
        <nukleolus  :molecule-collection="moleculeCollection" :atom-collection="atomCollection" :organism-collection="organismCollection" element="1"  v-model="value"  v-if="value[id].secondElement >= 1" :this-delay="value[id].secondElementDelay">
        </nukleolus>
        <nukleolus  :molecule-collection="moleculeCollection" :atom-collection="atomCollection" :organism-collection="organismCollection" element="2"  v-model="value"  v-if="value[id].thirdElement >= 1" :this-delay="value[id].thirdElementDelay">
        </nukleolus>

    </div>
    <div class="bestpractice__properties">
        <h3>bestpractice</h3>
        <form class="" action="index.html" method="post">
        <input name="name" class="atom__name" v-model="value[id].name">
        </form>
        <div>
        <select class="bestpractice__kind" v-model="value[id].firstElement">
           <option v-for="element in organismCollection" :value="element.orgid">
             {{ element.name }}
           </option>
        </select>
        <span class="connectedIt" v-if="value[id].firstElement >= 1">&</span>
        <select class="bestpractice__kind" v-model="value[id].secondElement" v-if="value[id].firstElement >= 1">
           <option  v-for="element in organismCollection" :value="element.orgid">
             {{ element.name }}
           </option>
        </select>
        <span class="connectedIt" v-if="value[id].secondElement >= 1">&</span>
        <select class="bestpractice__kind" v-model="value[id].thirdElement" v-if="value[id].secondElement >= 1">

           <option  v-for="element in organismCollection" :value="element.orgid">
             {{ element.name }}
           </option>
        </select>
        </div>


        <div class="bestpractice__timing">
            <div class="bestpractice__scaleDelay" v-if="value[id].firstElement >= 1">
                <h3>first delay {{value[id].firstElementDelay}}</h3>
                <input type="range" v-model="value[id].firstElementDelay" min="0" max="1000" step="10" defaultValue="0">
            </div>
            <div class="bestpractice__rotationDelay" v-if="value[id].secondElement >= 1">
                <h3>second delay {{value[id].secondElementDelay}}</h3>
                <input type="range" v-model="value[id].secondElementDelay" min="0" max="1000" step="10" defaultValue="0">
            </div>
            <div class="bestpractice__rotationDelay" v-if="value[id].thirdElement >= 1">
                <h3>third delay {{value[id].secondElementDelay}}</h3>
                <input type="range" v-model="value[id].secondElementDelay" min="0" max="1000" step="10" defaultValue="0">
            </div>
        </div>

    </div>
</div>
</template>
<script>
import nukleolus from './nukleolus_bp.vue'

export default {
    name: "bestpractice",
    components: {
        nukleolus
    },

    props: ['value', 'atomCollection', 'moleculeCollection', 'bestpractice', 'bestpracticeid', 'organismCollection'],
    data() {
        return {
            //
            copied: false,
            nukleolus: true,
            selected: ""

        }
    },
    mounted: function() {
        this.nukleolus = false

    },
    computed: {
        id() {
            return this.bestpracticeid
        },
        copyThisValue() {
            //return   this.value[this.id].name + this.value[this.id].orgid + "_id"
        },
        firstElementSelected() {
            let d = this.value[this.id].firstElement
            return !d ? null : this.organismCollection.find(element => element.orgid === d),
                this.organismCollection[d]

        },
        secondElementSelected() {
          let d = this.value[this.id].secondElement
          return !d ? null : this.organismCollection.find(element => element.orgid === d),
              this.organismCollection[d]
        },
        thirdElementSelected() {
          let d = this.value[this.id].thirdElement
          return !d ? null : this.organismCollection.find(element => element.orgid === d),
              this.organismCollection[d]
        },

      //Erstes Element
        firstElementSelectedId(){
          return this.firstElementSelected.firstMoleculeId
        },
        secondElementSelectedId(){
          return this.firstElementSelected.secondMoleculeId
        },
        thirdElementSelectedId(){
          return this.firstElementSelected.thirdMoleculeId
        },
        // molecule ebene
        firstSelectedMoleculeId(){
          return this.firstElementSelected.firstMoleculeId
        },
        secondSelectedMoleculeId(){
          return this.firstElementSelected.secondMoleculeId
        },
          //
        firstSelectedTranslateId(){
            return this.moleculeCollection[this.firstSelectedMoleculeId].translateId
          },
        firstSelectedscaleId() {
          return this.moleculeCollection[this.firstSelectedMoleculeId].scaleId
        },
        firstSelectedRotationId() {
          return this.moleculeCollection[this.firstSelectedMoleculeId].rotationId
        },
        firstSelectedOpacityId() {
          return this.moleculeCollection[this.firstSelectedMoleculeId].opacityId
        },
        secondSelectedscaleId() {
          return this.moleculeCollection[this.secondSelectedMoleculeId].scaleId
        },
        secondSelectedRotationId() {
          return this.moleculeCollection[this.secondSelectedMoleculeId].rotationId
        },
        secondSelectedOpacityId() {
          return this.moleculeCollection[this.secondSelectedMoleculeId].opacityId
        },
        secondSelectedTranslateId(){
          return this.moleculeCollection[this.secondSelectedMoleculeId].translateId
        },

        //Zweites Element
          firstElementSelectedIdSecond(){
            return this.secondElementSelected.firstMoleculeId
          },
          secondElementSelectedIdSecond(){
            return this.secondElementSelected.secondMoleculeId
          },
          thirdElementSelectedIdSecond(){
            return this.secondElementSelected.thirdMoleculeId
          },
          // molecule ebene
          firstSelectedMoleculeIdSecond(){
            return this.secondElementSelected.firstMoleculeId
          },
          secondSelectedMoleculeIdSecond(){
            return this.secondElementSelected.secondMoleculeId
          },
            //
          firstSelectedTranslateIdSecond(){
              return this.moleculeCollection[this.firstSelectedMoleculeIdSecond].translateId
            },
          firstSelectedscaleIdSecond() {
            return this.moleculeCollection[this.firstSelectedMoleculeIdSecond].scaleId
          },
          firstSelectedRotationIdSecond() {
            return this.moleculeCollection[this.firstSelectedMoleculeIdSecond].rotationId
          },
          firstSelectedOpacityIdSecond() {
            return this.moleculeCollection[this.firstSelectedMoleculeIdSecond].opacityId
          },
          secondSelectedscaleIdSecond() {
            return this.moleculeCollection[this.secondSelectedMoleculeIdSecond].scaleId
          },
          secondSelectedRotationIdSecond() {
            return this.moleculeCollection[this.secondSelectedMoleculeIdSecond].rotationId
          },
          secondSelectedOpacityIdSecond() {
            return this.moleculeCollection[this.secondSelectedMoleculeIdSecond].opacityId
          },
          secondSelectedTranslateIdSecond(){
            return this.moleculeCollection[this.secondSelectedMoleculeIdSecond].translateId
          }

          //



    },
    methods: {
        copyThis() {
            var clipboard = new Clipboard('#' + this.combineMoleculeCollection[this.id].name + this.combineMoleculeCollection[this.id].orgid)
            this.copied = true
            var self = this
            setTimeout(function() {
                self.copied = false;
            }, 1000);
        },
        //before animation
        beforeEnter: function(el) {
            el.style.width = this.atomCollection[this.firstSelectedscaleId].widthstart * this.value[this.id].viewPortScaleX + "px",
            el.style.height = this.atomCollection[this.firstSelectedscaleId].heightstart * this.value[this.id].viewPortScaleY + "px",
            el.style.transform = "rotateX("+ this.atomCollection[this.firstSelectedRotationId].rotationxstart +"deg)",
            el.style.transform = "rotateY("+ this.atomCollection[this.firstSelectedRotationId].rotationystart  +"deg)",
            el.style.transform = "rotateZ("+ this.atomCollection[this.firstSelectedRotationId].rotationzstart  +"deg)"

            if(this.atomCollection[this.firstSelectedTranslateId].translate || this.atomCollection[this.secondSelectedTranslateId].translate ){ el.style.opacity = 0}

            Velocity(el, {
                width: this.atomCollection[this.firstSelectedscaleId].widthstart * this.value[this.id].viewPortScaleX + "px",
                height: this.atomCollection[this.firstSelectedscaleId].heightstart * this.value[this.id].viewPortScaleY + "px",
                opacity: this.atomCollection[this.firstSelectedOpacityId].opacitystart / 100,
                rotateX: this.atomCollection[this.firstSelectedRotationId].rotationxstart,
                rotateY: this.atomCollection[this.firstSelectedRotationId].rotationystart,
                rotateZ: this.atomCollection[this.firstSelectedRotationId].rotationzstart,
                translateX:+this.atomCollection[this.firstSelectedTranslateId].translateXstart   *  this.value[this.id].viewPortScaleX - 180 *  this.value[this.id].viewPortScaleX + "px",
                translateY:+this.atomCollection[this.firstSelectedTranslateId].translateYstart   *  this.value[this.id].viewPortScaleY - 320 *  this.value[this.id].viewPortScaleX + "px"
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
              width: this.atomCollection[this.firstSelectedscaleId].widthfinal * this.value[this.id].viewPortScaleX  + "px",
              height: this.atomCollection[this.firstSelectedscaleId].heightfinal * this.value[this.id].viewPortScaleY + "px",
            }, {
                delay: 2000 + +this.moleculeCollection[this.firstSelectedMoleculeId].scaleDelay +
                 this.organismCollection[this.firstElementSelectedId].firstDelay,
                easing: this.atomCollection[this.firstSelectedscaleId].spacing,
                duration: this.atomCollection[this.firstSelectedscaleId].timing,
                complete: function() {
                   if (!vm.stop) vm.nukleolus = false
                }
            })

            Velocity(el, {
              rotateX: this.atomCollection[this.firstSelectedRotationId].rotationxfinal + "deg",
              rotateY: this.atomCollection[this.firstSelectedRotationId].rotationyfinal + "deg",
              rotateZ: this.atomCollection[this.firstSelectedRotationId].rotationzfinal + "deg",
            }, {
                delay: 2000 + +this.moleculeCollection[this.firstSelectedMoleculeId].rotationDelay +
                 this.organismCollection[this.firstElementSelectedId].firstDelay,
                easing: this.atomCollection[this.firstSelectedRotationId].spacing,
                queue: false,
                duration: this.atomCollection[this.firstSelectedRotationId].timing,
                complete: function() {
                   if (!vm.stop) vm.nukleolus = false
                }
            })
            Velocity(el, {
              opacity: this.atomCollection[this.firstSelectedOpacityId].opacityfinal / 100

            }, {
                delay: 2000 + +this.moleculeCollection[this.firstSelectedMoleculeId].opacityDelay +
                 this.organismCollection[this.firstElementSelectedId].firstDelay,
                easing: this.atomCollection[this.firstSelectedOpacityId].spacing,
                queue: false,
                duration: this.atomCollection[this.firstSelectedOpacityId].timing,
                complete: function() {
                   if (!vm.stop) vm.nukleolus = false

                }
            })
            Velocity(el, {
              translateX: this.atomCollection[this.firstSelectedTranslateId].translateXfinal *  this.value[this.id].viewPortScaleY  - 180 *  this.value[this.id].viewPortScaleX + "px",
              translateY: this.atomCollection[this.firstSelectedTranslateId].translateYfinal *  this.value[this.id].viewPortScaleY  - 320 *  this.value[this.id].viewPortScaleY + "px"
            }, {
              delay: 2000 + +this.moleculeCollection[this.firstSelectedMoleculeId].translateDelay +
               this.organismCollection[this.firstElementSelectedId].firstDelay,
              easing: this.atomCollection[this.firstSelectedTranslateId].spacing,
              queue: false,
              duration: this.atomCollection[this.firstSelectedTranslateId].timing,
              complete: function() {
                 if (!vm.stop) vm.nukleolus = false
                }
            })

      },
        //animation leave - just for restart
        leave: function(el, done) {
            var vm = this
            //console.log(this.firstSelected.firstMoleculeId)

            if (this.secondSelectedscaleId >= 1 || this.secondSelectedRotationId >= 1 || this.secondSelectedOpacityId >= 1 ) {
              if (this.secondSelectedscaleId >= 1){
                Velocity(el, {
                  width: this.atomCollection[this.secondSelectedscaleId].widthfinal * this.value[this.id].viewPortScaleX + "px",
                  height: this.atomCollection[this.secondSelectedscaleId].heightfinal * this.value[this.id].viewPortScaleY + "px",
                }, {
                    delay: +this.moleculeCollection[this.secondSelectedMoleculeId].scaleDelay +
                     this.organismCollection[this.firstElementSelectedId].secondDelay,
                    easing: this.atomCollection[this.secondSelectedscaleId].spacing,
                    duration: this.atomCollection[this.secondSelectedscaleId].timing,
                    complete: function() {

                      setTimeout(function(){
                        vm.nukleolus = true
                        }, 2000);
                    }
                })
              }
              if (this.secondSelectedRotationId >= 1){
                Velocity(el, {
                  rotateX: this.atomCollection[this.secondSelectedRotationId].rotationxfinal + "deg",
                  rotateY: this.atomCollection[this.secondSelectedRotationId].rotationyfinal + "deg",
                  rotateZ: this.atomCollection[this.secondSelectedRotationId].rotationzfinal + "deg",
                }, {
                    delay: +this.moleculeCollection[this.secondSelectedMoleculeId].rotationDelay +
                     this.organismCollection[this.firstElementSelectedId].secondDelay,
                    easing: this.atomCollection[this.secondSelectedRotationId].spacing,
                    queue: false,
                    duration: this.atomCollection[this.secondSelectedRotationId].timing,
                    complete: function() {

                      setTimeout(function(){
                        vm.nukleolus = true
                        }, 2000);
                    }
                })
              }
              if (this.secondSelectedOpacityId >= 1){
                Velocity(el, {
                  opacity: this.atomCollection[this.secondSelectedOpacityId].opacityfinal / 100

                }, {
                    delay: +this.moleculeCollection[this.secondSelectedMoleculeId].transitionDelay +
                     this.organismCollection[this.firstElementSelectedId].secondDelay,
                    easing: this.atomCollection[this.secondSelectedOpacityId].spacing,
                    queue: false,
                    duration: this.atomCollection[this.secondSelectedOpacityId].timing,
                    complete: function() {

                      setTimeout(function(){
                        vm.nukleolus = true
                        }, 2000);

                    }
                })
              }
              if (this.secondSelectedTranslateId >= 1){
                Velocity(el, {
                  translateX: this.atomCollection[this.secondSelectedTranslateId].translateXfinal *  this.value[this.id].viewPortScaleY  - 180 *  this.value[this.id].viewPortScaleX + "px",
                  translateY: this.atomCollection[this.secondSelectedTranslateId].translateYfinal *  this.value[this.id].viewPortScaleY  - 320 *  this.value[this.id].viewPortScaleY + "px"
                }, {
                  delay: +this.moleculeCollection[this.secondSelectedMoleculeId].translateDelay +
                   this.organismCollection[this.firstElementSelectedId].firstDelay,
                  easing: this.atomCollection[this.secondSelectedTranslateId].spacing,
                  queue: false,
                  duration: this.atomCollection[this.secondSelectedTranslateId].timing,
                  complete: function() {
                     if (!vm.stop) vm.nukleolus = false
                    }
                })
              }
          } else{
            Velocity(el, {
                backgroundColor: '#ffffff',
            }, {
                duration: 1,
                delay: "2000",
                complete: function() {
                    vm.nukleolus = true
                }
            })
          }
        },

      //   // second Molecule
      //   beforeEnterSecond: function(el) {
      //
      //       console.log(this.moleculeCollection[this.firstSelectedMoleculeIdSecond].scaleDelay)
      //       el.style.width = this.atomCollection[this.firstSelectedscaleIdSecond].widthstart * this.value[this.id].viewPortScaleX + "px",
      //       el.style.height = this.atomCollection[this.firstSelectedscaleIdSecond].heightstart * this.value[this.id].viewPortScaleY + "px",
      //       el.style.transform = "rotateX("+ this.atomCollection[this.firstSelectedRotationIdSecond].rotationxstart +"deg)",
      //       el.style.transform = "rotateY("+ this.atomCollection[this.firstSelectedRotationIdSecond].rotationystart  +"deg)",
      //       el.style.transform = "rotateZ("+ this.atomCollection[this.firstSelectedRotationIdSecond].rotationzstart  +"deg)"
      //
      //       if(this.atomCollection[this.firstSelectedTranslateIdSecond].translate || this.atomCollection[this.secondSelectedTranslateIdSecond].translate ){ el.style.opacity = 0}
      //
      //       Velocity(el, {
      //           width: this.atomCollection[this.firstSelectedscaleIdSecond].widthstart * this.value[this.id].viewPortScaleX + "px",
      //           height: this.atomCollection[this.firstSelectedscaleIdSecond].heightstart * this.value[this.id].viewPortScaleY + "px",
      //           opacity: this.atomCollection[this.firstSelectedOpacityIdSecond].opacitystart / 100,
      //           rotateX: this.atomCollection[this.firstSelectedRotationIdSecond].rotationxstart,
      //           rotateY: this.atomCollection[this.firstSelectedRotationIdSecond].rotationystart,
      //           rotateZ: this.atomCollection[this.firstSelectedRotationIdSecond].rotationzstart,
      //           translateX:+this.atomCollection[this.firstSelectedTranslateIdSecond].translateXstart   *  this.value[this.id].viewPortScaleX - 180 *  this.value[this.id].viewPortScaleX + "px",
      //           translateY:+this.atomCollection[this.firstSelectedTranslateIdSecond].translateYstart   *  this.value[this.id].viewPortScaleY - 320 *  this.value[this.id].viewPortScaleX + "px"
      //       }, {
      //           duration: 0,
      //           delay: "0",
      //           queue: false
      //
      //       })
      //
      //   },
      //
      //   //animation enter
      //   enterSecond: function(el, done) {
      //       var vm = this
      //
      //       Velocity(el, {
      //         width: this.atomCollection[this.secondSelectedscaleIdSecond].widthfinal * this.value[this.id].viewPortScaleX  + "px",
      //         height: this.atomCollection[this.secondSelectedscaleIdSecond].heightfinal * this.value[this.id].viewPortScaleY + "px",
      //       }, {
      //           delay: 2000,
      //           // + +this.moleculeCollection[this.secondSelectedMoleculeIdSecond].scaleDelay +
      //         //  this.organismCollection[this.firstElementSelectedIdSecond].firstDelay,
      //           easing: this.atomCollection[this.secondSelectedscaleIdSecond].spacing,
      //           duration: this.atomCollection[this.secondSelectedscaleIdSecond].timing,
      //           complete: function() {
      //              if (!vm.stop) vm.nukleolus = false
      //           }
      //       })
      //
      //       Velocity(el, {
      //         rotateX: this.atomCollection[this.firstSelectedRotationIdSecond].rotationxfinal + "deg",
      //         rotateY: this.atomCollection[this.firstSelectedRotationIdSecond].rotationyfinal + "deg",
      //         rotateZ: this.atomCollection[this.firstSelectedRotationIdSecond].rotationzfinal + "deg",
      //       }, {
      //           delay: 2000 + +this.moleculeCollection[this.firstSelectedMoleculeIdSecond].rotationDelay +
      //            this.organismCollection[this.firstElementSelectedIdSecond].firstDelay,
      //           easing: this.atomCollection[this.firstSelectedRotationIdSecond].spacing,
      //           queue: false,
      //           duration: this.atomCollection[this.firstSelectedRotationIdSecond].timing,
      //           complete: function() {
      //              if (!vm.stop) vm.nukleolus = false
      //           }
      //       })
      //       Velocity(el, {
      //         opacity: this.atomCollection[this.firstSelectedOpacityIdSecond].opacityfinal / 100
      //
      //       }, {
      //           delay: 2000 + +this.moleculeCollection[this.firstSelectedMoleculeIdSecond].opacityDelay +
      //            this.organismCollection[this.firstElementSelectedIdSecond].firstDelay,
      //           easing: this.atomCollection[this.firstSelectedOpacityIdSecond].spacing,
      //           queue: false,
      //           duration: this.atomCollection[this.firstSelectedOpacityIdSecond].timing,
      //           complete: function() {
      //              if (!vm.stop) vm.nukleolus = false
      //
      //           }
      //       })
      //       Velocity(el, {
      //         translateX: this.atomCollection[this.firstSelectedTranslateIdSecond].translateXfinal *  this.value[this.id].viewPortScaleY  - 180 *  this.value[this.id].viewPortScaleX + "px",
      //         translateY: this.atomCollection[this.firstSelectedTranslateIdSecond].translateYfinal *  this.value[this.id].viewPortScaleY  - 320 *  this.value[this.id].viewPortScaleY + "px"
      //       }, {
      //         delay: 2000 + +this.moleculeCollection[this.firstSelectedMoleculeIdSecond].translateDelay +
      //          this.organismCollection[this.firstElementSelectedIdSecond].firstDelay,
      //         easing: this.atomCollection[this.firstSelectedTranslateIdSecond].spacing,
      //         queue: false,
      //         duration: this.atomCollection[this.firstSelectedTranslateIdSecond].timing,
      //         complete: function() {
      //            if (!vm.stop) vm.nukleolus = false
      //           }
      //       })
      //
      // },
      //   //animation leave - just for restart
      //   leaveSecond: function(el, done) {
      //       var vm = this
      //       //console.log(this.firstSelected.firstMoleculeId)
      //
      //       if (this.secondSelectedscaleId >= 1 || this.secondSelectedRotationId >= 1 || this.secondSelectedOpacityId >= 1 ) {
      //         if (this.secondSelectedscaleId >= 1){
      //           Velocity(el, {
      //             width: this.atomCollection[this.secondSelectedscaleIdSecond].widthfinal * this.value[this.id].viewPortScaleX + "px",
      //             height: this.atomCollection[this.secondSelectedscaleIdSecond].heightfinal * this.value[this.id].viewPortScaleY + "px",
      //           }, {
      //               delay: +this.moleculeCollection[this.secondSelectedMoleculeIdSecond].scaleDelay +
      //                this.organismCollection[this.firstElementSelectedIdSecond].secondDelay,
      //               easing: this.atomCollection[this.secondSelectedscaleIdSecond].spacing,
      //               duration: this.atomCollection[this.secondSelectedscaleIdSecond].timing,
      //               complete: function() {
      //
      //                 setTimeout(function(){
      //                   vm.nukleolus = true
      //                   }, 2000);
      //               }
      //           })
      //         }
      //         if (this.secondSelectedRotationId >= 1){
      //           Velocity(el, {
      //             rotateX: this.atomCollection[this.secondSelectedRotationIdSecond].rotationxfinal + "deg",
      //             rotateY: this.atomCollection[this.secondSelectedRotationIdSecond].rotationyfinal + "deg",
      //             rotateZ: this.atomCollection[this.secondSelectedRotationIdSecond].rotationzfinal + "deg",
      //           }, {
      //               delay: +this.moleculeCollection[this.secondSelectedMoleculeIdSecond].rotationDelay +
      //                this.organismCollection[this.firstElementSelectedIdSecond].secondDelay,
      //               easing: this.atomCollection[this.secondSelectedRotationIdSecond].spacing,
      //               queue: false,
      //               duration: this.atomCollection[this.secondSelectedRotationIdSecond].timing,
      //               complete: function() {
      //
      //                 setTimeout(function(){
      //                   vm.nukleolus = true
      //                   }, 2000);
      //               }
      //           })
      //         }
      //         if (this.secondSelectedOpacityId >= 1){
      //           Velocity(el, {
      //             opacity: this.atomCollection[this.secondSelectedOpacityIdSecond].opacityfinal / 100
      //
      //           }, {
      //               delay: +this.moleculeCollection[this.secondSelectedMoleculeIdSecond].transitionDelay +
      //                this.organismCollection[this.firstElementSelectedIdSecond].secondDelay,
      //               easing: this.atomCollection[this.secondSelectedOpacityIdSecond].spacing,
      //               queue: false,
      //               duration: this.atomCollection[this.secondSelectedOpacityIdSecond].timing,
      //               complete: function() {
      //
      //                 setTimeout(function(){
      //                   vm.nukleolus = true
      //                   }, 2000);
      //
      //               }
      //           })
      //         }
      //         if (this.secondSelectedTranslateId >= 1){
      //           Velocity(el, {
      //             translateX: this.atomCollection[this.secondSelectedTranslateIdSecond].translateXfinal *  this.value[this.id].viewPortScaleY  - 180 *  this.value[this.id].viewPortScaleX + "px",
      //             translateY: this.atomCollection[this.secondSelectedTranslateIdSecond].translateYfinal *  this.value[this.id].viewPortScaleY  - 320 *  this.value[this.id].viewPortScaleY + "px"
      //           }, {
      //             delay: +this.moleculeCollection[this.secondSelectedMoleculeIdSecond].translateDelay +
      //              this.organismCollection[this.firstElementSelectedIdSecond].firstDelay,
      //             easing: this.atomCollection[this.secondSelectedTranslateIdSecond].spacing,
      //             queue: false,
      //             duration: this.atomCollection[this.secondSelectedTranslateIdSecond].timing,
      //             complete: function() {
      //                if (!vm.stop) vm.nukleolus = false
      //               }
      //           })
      //         }
      //     } else{
      //       Velocity(el, {
      //           backgroundColor: '#ffffff',
      //       }, {
      //           duration: 1,
      //           delay: "2000",
      //           complete: function() {
      //               vm.nukleolus = true
      //           }
      //       })
      //     }
      //   }

    }

}
</script>
