<template name="organism">
<div class="molecule__bond">

    <div class="molecule__viewer">
        <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
            <div class="molecule__nukleolus" v-if="nukleolus"></div>
        </transition>
    </div>
    <div class="molecule__properties">
      <h3>molecule</h3>
      <form class="" action="index.html" method="post">
        <input name="name" class="atom__name" v-model="value[id].name" >
      </form>
      <div>
        <select  class="atom__kind" v-model="value[id].firstMoleculeId">
           <option  v-for="molecule in moleculeCollection" :value="molecule.molid">
             {{ molecule.name }}
           </option>
        </select>
        <select  class="atom__kind" v-model="value[id].secondMoleculeId">
           <option  v-for="molecule in moleculeCollection" :value="molecule.molid">
             {{ molecule.name }}
           </option>
        </select>
        <select  class="atom__kind" v-model="value[id].thirdMoleculeId">
           <option  v-for="molecule in moleculeCollection" :value="molecule.molid">
             {{ molecule.name }}
           </option>
        </select>
    </div>


        <div class="molecule__timing">

          <!-- <div class="molecule__sizeDelay" v-if="value[id].sizeId >= 1">
            <h3>size delay {{value[id].sizeDelay}}</h3>
            <input type="range" v-model="value[id].sizeDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
          <div class="molecules__rotationDelay" v-if="value[id].rotationId >= 1">
            <h3>rotation delay {{value[id].rotationDelay}}</h3>
            <input type="range" v-model="value[id].rotationDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
          <div class="molecules__opacityDelay" v-if="value[id].opacityId >= 1">
            <h3>opacity delay {{value[id].opacityDelay}}</h3>
            <input  type="range" v-model="value[id].opacityDelay" min="0" max="1000" step="10" defaultValue="0">
          </div> -->
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
          firstSelectedId: 0,
          secondSelectedId: 0,
          thirdSelectedId: 0,
          fourthSelectedId: 0,
          //
          nukleolus: true,
          selected: "",

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
        let d = this.value[0].firstMoleculeId
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
                rotateX: atomCollection[this.firstSelectedRotationId].rotationxstart,
                rotateY: atomCollection[this.firstSelectedRotationId].rotationystart,
                rotateZ: atomCollection[this.firstSelectedRotationId].rotationzstart
            }, {
                duration: 0,
                delay: "0",
                queue: false

            })

        },

        //animation enter
        enter: function(el, done) {
            var vm = this
            //width
            Velocity(el, {
              width: this.atomCollection[this.firstSelectedSizeId].widthfinal + "%",
              height: this.atomCollection[this.firstSelectedSizeId].heightfinal + "%"

            }, {
                delay: 2000 + +this.firstSelected.sizeDelay,
                easing: this.atomCollection[this.firstSelectedSizeId].spacing,
                duration: this.atomCollection[this.firstSelectedSizeId].timing,
                complete: function() {
                   done()
                   if (!vm.stop) vm.nukleolus = false
                }
            })


            //height


          //rotationx
          //rotationY
          //rotation/
          //opacity



            Velocity(el, {

              rotateX: this.atomCollection[this.firstSelectedRotationId].rotationxfinal + "deg",
              rotateY: this.atomCollection[this.firstSelectedRotationId].rotationyfinal + "deg",
              rotateZ: this.atomCollection[this.firstSelectedRotationId].rotationzfinal + "deg"
            }, {
                delay: 2000 + +this.firstSelected.rotationDelay,
                easing: this.atomCollection[this.firstSelectedRotationId].spacing,
                duration: this.atomCollection[this.firstSelectedRotationId].timing,
                queue: false,
                complete: function() {
                   done()
                   if (!vm.stop) vm.nukleolus = false
                }
            })
            Velocity(el, {
              opacity: this.atomCollection[this.firstSelectedOpacityId].opacityfinal / 100,
            }, {
                delay: 2000 + +this.firstSelected.opacityDelay,
                easing: this.atomCollection[this.firstSelectedOpacityId].spacing,
                duration: this.atomCollection[this.firstSelectedOpacityId].timing,
                queue: false,
                complete: function() {
                   done()
                   if (!vm.stop) vm.nukleolus = false
                }
            })

            //secondSelected
            // Velocity(el, {
            //   width: this.atomCollection[this.secondSelectedSizeId].widthstart + "%",
            //   height: this.atomCollection[this.secondSelectedSizeId].heightstart + "%",
            //   rotateX: this.atomCollection[this.secondSelectedRotationId].rotationxstart + "deg",
            //   rotateY: this.atomCollection[this.secondSelectedRotationId].rotationystart + "deg",
            //   rotateZ: this.atomCollection[this.secondSelectedRotationId].rotationzstart + "deg",
            //   opacity: this.atomCollection[this.secondSelectedOpacityId].opacitystart / 100,
            // }, {
            //     delay: 2000 + +this.secondSelected.opacityDelay,
            //     queue: null,
            //     complete: function() {
            //        done()
            //        if (!vm.stop) vm.nukleolus = false
            //     }
            // })
            Velocity(el, {
              width: this.atomCollection[this.secondSelectedSizeId].widthfinal + "%",
              height: this.atomCollection[this.secondSelectedSizeId].heightfinal + "%"

            }, {
                delay: 2000 + +this.secondSelected.sizeDelay,
                easing: this.atomCollection[this.secondSelectedSizeId].spacing,
                duration: this.atomCollection[this.secondSelectedSizeId].timing,
                complete: function() {
                   done()
                   if (!vm.stop) vm.nukleolus = false
                }
            })
            Velocity(el, {

              rotateX: this.atomCollection[this.secondSelectedRotationId].rotationxfinal + "deg",
              rotateY: this.atomCollection[this.secondSelectedRotationId].rotationyfinal + "deg",
              rotateZ: this.atomCollection[this.secondSelectedRotationId].rotationzfinal + "deg"
            }, {
                delay: 2000 + +this.secondSelected.rotationDelay,
                easing: this.atomCollection[this.secondSelectedRotationId].spacing,
                duration: this.atomCollection[this.secondSelectedRotationId].timing,
                queue: false,
                complete: function() {
                   done()
                   if (!vm.stop) vm.nukleolus = false
                }
            })
            Velocity(el, {
              opacity: this.atomCollection[this.secondSelectedOpacityId].opacityfinal / 100,
            }, {
                delay: 2000 + +this.secondSelected.opacityDelay,
                easing: this.atomCollection[this.secondSelectedOpacityId].spacing,
                duration: this.atomCollection[this.secondSelectedOpacityId].timing,
                queue: false,
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
