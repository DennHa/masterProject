<template name="organism">
<div class="organism__bond">

    <div class="organism__viewer">
      <div class="molecule__organismWrapper">
        <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
            <div class="molecule__nukleolus" v-if="nukleolus"></div>
        </transition>
      </div>
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
    </div>


        <div class="organism__timing">

          <div class="organism__scaleDelay" v-if="this.firstSelectedscaleId >= 1 || this.firstSelectedRotationId >= 1 || this.firstSelectedOpacityId >= 1">
            <h3>first delay {{value[id].firstDelay}}</h3>
            <input type="range" v-model="value[id].firstDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
        </div>
        <div class="organism__timing">
          <div class="organism__rotationDelay" v-if="this.secondSelectedscaleId >= 1 || this.secondSelectedRotationId >= 1 || this.secondSelectedOpacityId >= 1">
            <h3>second delay {{value[id].secondDelay}}</h3>
            <input type="range" v-model="value[id].secondDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
        </div>
        <div class="organism__timing">
          <div class="organism__opacityDelay" v-if="this.thirdSelectedscaleId >= 1 || this.thirdSelectedRotationId >= 1 || this.thirdSelectedOpacityId >= 1">
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

      firstSelectedscaleId(){
        return this.firstSelected.scaleId
      },
      firstSelectedRotationId(){
        return this.firstSelected.rotationId
      },
      firstSelectedOpacityId(){
        return this.firstSelected.opacityId
      },
      secondSelectedscaleId(){
        return this.secondSelected.scaleId
      },
      secondSelectedRotationId(){
        return this.secondSelected.rotationId
      },
      secondSelectedOpacityId(){
        return this.secondSelected.opacityId
      },
      thirdSelectedscaleId(){
        return this.thirdSelected.scaleId
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
            el.style.width = this.atomCollection[this.firstSelectedscaleId].widthstart * this.value[this.id].viewPortScaleX + "px",
            el.style.height = this.atomCollection[this.firstSelectedscaleId].heightstart * this.value[this.id].viewPortScaleY + "px",
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

            Velocity(el, {
              width: this.atomCollection[this.firstSelectedscaleId].widthfinal * this.value[this.id].viewPortScaleX  + "px",
              height: this.atomCollection[this.firstSelectedscaleId].heightfinal * this.value[this.id].viewPortScaleY + "px",
            }, {
                delay: 2000 + +this.firstSelected.scaleDelay +
                 +this.value[this.id].firstDelay,
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

      },
        //animation leave - just for restart
        leave: function(el, done) {
            var vm = this
            if (this.secondSelectedscaleId >= 1 || this.secondSelectedRotationId >= 1 || this.secondSelectedOpacityId >= 1 ) {
              if (this.secondSelectedscaleId >= 1){
                Velocity(el, {
                  width: this.atomCollection[this.secondSelectedscaleId].widthfinal * this.value[this.id].viewPortScaleX + "px",
                  height: this.atomCollection[this.secondSelectedscaleId].heightfinal * this.value[this.id].viewPortScaleY + "px",
                }, {
                    delay: +this.secondSelected.scaleDelay +
                     +this.value[this.id].secondDelay,
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
              }
              if (this.secondSelectedOpacityId >= 1){
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
