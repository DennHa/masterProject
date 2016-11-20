<template name="nukleolus">
  <div class="molecule__bestpracticeWrapper">
      <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
          <div class="molecule__nukleolus" v-if="nukleolus"></div>
      </transition>
  </div>
</template>
<script>
export default {
    name: "nukleolus",


    props: ['value', 'atomCollection', 'moleculeCollection', 'bestpractice', 'nukleolusid', 'organismCollection', 'firstElementSelected', 'secondElementSelected', 'element', 'thisDelay'],
    data() {
        return {
            nukleolus: true,
            selected: ""

        }
    },
    mounted: function() {
        this.nukleolus = false

    },
    computed: {
        id() {
            return 0
        },
        firstElementSelected() {
          if (this.element == 0){
            var d = this.value[this.id].firstElement
          }
          else if (this.element== 1) {
            var d = this.value[this.id].secondElement
          }
          else if (this.element== 2) {
            var d = this.value[this.id].thirdElement
          }
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
        }
    },
    methods: {

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
                 this.organismCollection[this.firstElementSelectedId].firstDelay + +this.thisDelay,
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
                 this.organismCollection[this.firstElementSelectedId].firstDelay + +this.thisDelay,
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
               this.organismCollection[this.firstElementSelectedId].firstDelay + +this.thisDelay,
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
        }

    }

}
</script>
