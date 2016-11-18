<template name="organism">
<div class="organism__bond">

    <div class="organism__viewer">
        <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
            <div class="molecule__nukleolus" v-if="nukleolus"></div>
        </transition>
    </div>
    <div class="organism__properties">
      <h3>organism</h3>
      <form class="" action="index.html" method="post">
        <input name="name" class="atom__name" v-model="value[id].name" >
      </form>
      <div>
        <select  class="organism__kind" v-model="value[id].firstMoleculeId">
           <option  v-for="molecule in moleculeCollection" :value="molecule.molid">
             {{ molecule.name }}
           </option>
        </select>
        <span class="connectedIt">+</span>
        <select  class="organism__kind" v-model="value[id].secondMoleculeId">
           <option  v-for="molecule in moleculeCollection" :value="molecule.molid">
             {{ molecule.name }}
           </option>
        </select>
        <!-- <span class="connectedIt">+</span>
        <select  class="atom__kind" v-model="value[id].thirdMoleculeId">
           <option  v-for="molecule in moleculeCollection" :value="molecule.molid">
             {{ molecule.name }}
           </option>
        </select> -->
    </div>


        <div class="organism__timing">

          <div class="organism__sizeDelay" v-if="this.firstSelectedSizeId >= 1 || this.firstSelectedRotationId >= 1 || this.firstSelectedOpacityId >= 1">
            <h3>first delay {{value[id].firstDelay}}</h3>
            <input type="range" v-model="value[id].firstDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
        </div>
        <div class="organism__timing">
          <div class="organism__rotationDelay" v-if="this.secondSelectedSizeId >= 1 || this.secondSelectedRotationId >= 1 || this.secondSelectedOpacityId >= 1">
            <h3>second delay {{value[id].secondDelay}}</h3>
            <input type="range" v-model="value[id].secondDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
        </div>
        <div class="organism__timing">
          <div class="organism__opacityDelay" v-if="this.thirdSelectedSizeId >= 1 || this.thirdSelectedRotationId >= 1 || this.thirdSelectedOpacityId >= 1">
            <h3>third delay {{value[id].thirdDelay}}</h3>
            <input  type="range" v-model="value[id].thirdDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
        </div>
    </div>
</div>
</template>
<script>


export default {
    name: "organism",

    props: ['value', 'atomCollection', 'moleculeCollection', 'organism', 'organismid'],
    data() {
        return {
          //
          nukleolus: true,
          selected: ""

        }
    },
    mounted: function() {
      this.nukleolus = false

    },
    computed: {
      id(){
        return this.organismid
      },
      firstSelected(){
        let d = this.value[this.id].firstMoleculeId
        return !d ? null : this.moleculeCollection.find(molecule => molecule.molid === d),
        this.moleculeCollection[d]

      },
      secondSelected(){
        let d = this.value[this.id].secondMoleculeId
        return !d ? null : this.moleculeCollection.find(molecule => molecule.molid === d),
        this.moleculeCollection[d]
      },
      thirdSelected(){
        let d = this.value[this.id].thirdMoleculeId
        return !d ? null : this.moleculeCollection.find(molecule => molecule.molid === d),
        this.moleculeCollection[d]
      },

      firstSelectedSizeId(){
        return this.firstSelected.sizeId
      },
      firstSelectedRotationId(){
        return this.firstSelected.rotationId
      },
      firstSelectedOpacityId(){
        return this.firstSelected.opacityId
      },
      secondSelectedSizeId(){
        return this.secondSelected.sizeId
      },
      secondSelectedRotationId(){
        return this.secondSelected.rotationId
      },
      secondSelectedOpacityId(){
        return this.secondSelected.opacityId
      },
      thirdSelectedSizeId(){
        return this.thirdSelected.sizeId
      },
      thirdSelectedRotationId(){
        return this.thirdSelected.rotationId
      },
      thirdSelectedOpacityId(){
        return this.thirdSelected.opacityId
      }

    },
    methods: {

        //before animation
        beforeEnter: function(el) {
            el.style.width = this.atomCollection[this.firstSelectedSizeId].widthstart + "%",
            el.style.height = this.atomCollection[this.firstSelectedSizeId].heightstart + "%",
            el.style.transform = "rotateX("+ this.atomCollection[this.firstSelectedRotationId].rotationxstart +"deg)",
            el.style.transform = "rotateY("+ this.atomCollection[this.firstSelectedRotationId].rotationystart  +"deg)",
            el.style.transform = "rotateZ("+ this.atomCollection[this.firstSelectedRotationId].rotationzstart  +"deg)",
            el.style.opacity = this.atomCollection[this.firstSelectedOpacityId].opacitystart / 100,
            Velocity(el, {
                rotateX: this.atomCollection[this.firstSelectedRotationId].rotationxstart,
                rotateY: this.atomCollection[this.firstSelectedRotationId].rotationystart,
                rotateZ: this.atomCollection[this.firstSelectedRotationId].rotationzstart
            }, {
                duration: 0,
                delay: "0",
                queue: false

            })

        },

        //animation enter
        enter: function(el, done) {
            var vm = this

            // //animation start
            // Velocity(el, {
            //   width: this.atomCollection[this.firstSelectedSizeId].widthstart + "%",
            //   height: this.atomCollection[this.firstSelectedSizeId].heightstart + "%",
            //   rotateX: this.atomCollection[this.firstSelectedRotationId].rotationxszart + "deg",
            //   rotateY: this.atomCollection[this.firstSelectedRotationId].rotationyszart + "deg",
            //   rotateZ: this.atomCollection[this.firstSelectedRotationId].rotationzszart + "deg",
            //   opacity: this.atomCollection[this.firstSelectedOpacityId].opacityfinal / 100
            //
            // }, {
            //     delay: 2000 +this.firstSelected.firstDelay,
            //     //easing: this.atomCollection[this.firstSelectedSizeId].spacing,
            //     duration: 3000,
            //
            //     complete: function() {
            //        done()
            //        if (!vm.stop) vm.nukleolus = false
            //     }
            // })

            //animation firstSelected
            Velocity(el, {
              width: this.atomCollection[this.firstSelectedSizeId].widthfinal + "%",
              height: this.atomCollection[this.firstSelectedSizeId].heightfinal + "%",
            }, {
                delay: 2000 + +this.firstSelected.sizeDelay +
                 +this.value[this.id].firstDelay,
                easing: this.atomCollection[this.firstSelectedSizeId].spacing,
                duration: this.atomCollection[this.firstSelectedSizeId].timing,
                complete: function() {
                   if (!vm.stop) vm.nukleolus = false
                }
            })

            Velocity(el, {
              rotateX: this.atomCollection[this.firstSelectedRotationId].rotationxfinal + "deg",
              rotateY: this.atomCollection[this.firstSelectedRotationId].rotationyfinal + "deg",
              rotateZ: this.atomCollection[this.firstSelectedRotationId].rotationzfinal + "deg",
            }, {
                delay: 2000 + +this.firstSelected.rotationDelay +
                 +this.value[this.id].firstDelay,
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
                delay: 2000 + +this.firstSelected.opacityDelay +
                 +this.value[this.id].firstDelay,
                easing: this.atomCollection[this.firstSelectedOpacityId].spacing,
                queue: false,
                duration: this.atomCollection[this.firstSelectedOpacityId].timing,
                complete: function() {
                   if (!vm.stop) vm.nukleolus = false

                }
            })

        //     //secondSelected

        //       //size start
        //       Velocity(el, {
        //         width: this.atomCollection[this.secondSelectedSizeId].widthstart + "%",
        //         height: this.atomCollection[this.secondSelectedSizeId].heightstart + "%",
        //         rotateX: this.atomCollection[this.secondSelectedRotationId].rotationxstart + "deg",
        //         rotateY: this.atomCollection[this.secondSelectedRotationId].rotationystart + "deg",
        //         rotateZ: this.atomCollection[this.secondSelectedRotationId].rotationzstart + "deg",
        //         opacity: this.atomCollection[this.secondSelectedOpacityId].opacitystart / 100
        //
        //       }, {
        //           delay:  +this.value[this.id].secondDelay, //
        //           easing: this.atomCollection[this.secondSelectedSizeId].spacing,
        //           queue: "b",
        //           duration: 0,
        //       })
        //       //size final
        //       Velocity(el, {
        //         width: this.atomCollection[this.secondSelectedSizeId].widthfinal + "%",
        //         height: this.atomCollection[this.secondSelectedSizeId].heightfinal + "%",
        //       }, {
        //
        //           easing: this.atomCollection[this.secondSelectedSizeId].spacing,
        //           duration: this.atomCollection[this.secondSelectedSizeId].timing,
        //           queue: "b",
        //           complete: function() {
        //              done()
        //              if (!vm.stop) vm.nukleolus = false
        //
        //           }
        //       })
        //       Velocity(el, {
        //
        //         rotateX: this.atomCollection[this.secondSelectedRotationId].rotationxfinal + "deg",
        //         rotateY: this.atomCollection[this.secondSelectedRotationId].rotationyfinal + "deg",
        //         rotateZ: this.atomCollection[this.secondSelectedRotationId].rotationzfinal + "deg",
        //
        //       }, {
        //
        //           easing: this.atomCollection[this.secondSelectedSizeId].spacing,
        //           duration: this.atomCollection[this.secondSelectedSizeId].timing,
        //           queue: "b",
        //           queue: false,
        //           complete: function() {
        //              done()
        //              if (!vm.stop) vm.nukleolus = false
        //           }
        //       })
        //       Velocity(el, {
        //         opacity: this.atomCollection[this.secondSelectedOpacityId].opacityfinal / 100
        //       }, {
        //
        //           easing: this.atomCollection[this.secondSelectedSizeId].spacing,
        //           duration: this.atomCollection[this.secondSelectedSizeId].timing,
        //           queue: "b",
        //           complete: function() {
        //              done()
        //              if (!vm.stop) vm.nukleolus = false
        //           }
        //       })
        //     }
        //
        //     //thirdSelected
        //     if (this.thirdSelectedSizeId >= 1 || this.thirdSelectedRotationId >= 1 || this.thirdSelectedOpacityId >= 1 ) {
        //       //size start
        //       Velocity(el, {
        //
        //         opacity: this.atomCollection[this.thirdSelectedOpacityId].opacitystart / 100
        //
        //       }, {
        //           delay: 0, //<-- hier muss nachher noch der slider rein
        //           easing: this.atomCollection[this.thirdSelectedSizeId].spacing,
        //           duration: this.atomCollection[this.thirdSelectedSizeId].timing,
        //           complete: function() {
        //              done()
        //              if (!vm.stop) vm.nukleolus = false
        //           }
        //       })
        //       //size final
        //       Velocity(el, {
        //         width: this.atomCollection[this.thirdSelectedSizeId].widthfinal + "%",
        //         height: this.atomCollection[this.thirdSelectedSizeId].heightfinal + "%",
        //         rotateX: this.atomCollection[this.thirdSelectedRotationId].rotationxfinal + "deg",
        //         rotateY: this.atomCollection[this.thirdSelectedRotationId].rotationyfinal + "deg",
        //         rotateZ: this.atomCollection[this.thirdSelectedRotationId].rotationzfinal + "deg",
        //         opacity: this.atomCollection[this.thirdSelectedOpacityId].opacityfinal / 100
        //       }, {
        //           delay: +this.value[this.id].thirdDelay,
        //           easing: this.atomCollection[this.thirdSelectedSizeId].spacing,
        //           duration: this.atomCollection[this.thirdSelectedSizeId].timing,
        //           complete: function() {
        //              done()
        //              if (!vm.stop) vm.nukleolus = false
        //           }
        //       })
        //     }
        //
        // },
      },
        //animation leave - just for restart
        leave: function(el, done) {
            var vm = this
            if (this.secondSelectedSizeId >= 1 || this.secondSelectedRotationId >= 1 || this.secondSelectedOpacityId >= 1 ) {
              Velocity(el, {
                width: this.atomCollection[this.secondSelectedSizeId].widthfinal + "%",
                height: this.atomCollection[this.secondSelectedSizeId].heightfinal + "%",
              }, {
                  delay: +this.secondSelected.sizeDelay +
                   +this.value[this.id].secondDelay,
                  easing: this.atomCollection[this.secondSelectedSizeId].spacing,
                  duration: this.atomCollection[this.secondSelectedSizeId].timing,
                  complete: function() {

                    setTimeout(function(){
                      vm.nukleolus = true
                      }, 2000);
                  }
              })

              Velocity(el, {
                rotateX: this.atomCollection[this.secondSelectedRotationId].rotationxfinal + "deg",
                rotateY: this.atomCollection[this.secondSelectedRotationId].rotationyfinal + "deg",
                rotateZ: this.atomCollection[this.secondSelectedRotationId].rotationzfinal + "deg",
              }, {
                  delay: +this.secondSelected.rotationDelay +
                   +this.value[this.id].secondDelay,
                  easing: this.atomCollection[this.secondSelectedRotationId].spacing,
                  queue: false,
                  duration: this.atomCollection[this.secondSelectedRotationId].timing,
                  complete: function() {

                    setTimeout(function(){
                      vm.nukleolus = true
                      }, 2000);
                  }
              })
              Velocity(el, {
                opacity: this.atomCollection[this.secondSelectedOpacityId].opacityfinal / 100

              }, {
                  delay: +this.secondSelected.opacityDelay +
                   +this.value[this.id].secondDelay,
                  easing: this.atomCollection[this.secondSelectedOpacityId].spacing,
                  queue: false,
                  duration: this.atomCollection[this.secondSelectedOpacityId].timing,
                  complete: function() {

                    setTimeout(function(){
                      vm.nukleolus = true
                      }, 2000);

                  }
              })
          } else{
            Velocity(el, {
                backgroundColor: '#ffffff',
            }, {
                duration: 1,
                delay: "2000",
                complete: function() {
                  setTimeout(function(){
                    vm.nukleolus = true
                    }, 2000);

                }
            })
          }
        }

    }

}

</script>
