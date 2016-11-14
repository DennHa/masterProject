<template name="molecule">
<div class="molecule__bond">

    <div class="molecule__viewer">
        <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
            <div class="molecule__nukleolus" v-if="nukleolus"></div>
        </transition>
    </div>
    <div class="molecule__properties">
      <form class="" action="index.html" method="post">
        <input name="name" class="atom__name" v-model="value[id].name" >
      </form>
      <div>
        <select  class="atom__kind" v-model="firstSelectedId">
           <option v-if="atom.widthfinal" v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>
        <select  class="atom__kind" v-model="secondSelectedId">
           <option v-if="atom.rotationzfinal" v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>
        <select  class="atom__kind" v-model="thirdSelectedId">
           <option v-if="atom.opacityfinal" v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>
    </div>


        <div class="molecule__timing">

          <div class="molecule__sizeDelay" v-if="firstSelectedId >= 1">
            <h3>size delay {{sizeDelay}}</h3>
            <input type="range" v-model="sizeDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
          <div class="molecules__rotationDelay" v-if="secondSelectedId >= 1">
            <h3>rotation delay {{rotationDelay}}</h3>
            <input type="range" v-model="rotationDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
          <div class="molecules__opacityDelay" v-if="thirdSelectedId >= 1">
            <h3>opacity delay {{opacityDelay}}</h3>
            <input  type="range" v-model="opacityDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>


            <!-- <form>
                <input name="time" v-model="value[id].timing" value="" type="number">
                <select v-model="value[id].spacing" class="atom__kind">
                   <option v-for="ease in easings" v-bind:value="ease.easeFunction"  >
                     {{ ease.easeFunction }}
                   </option>
              </select>
            </form> -->
        </div>
    </div>
</div>
</template>
<script>


export default {
    name: "molecules",

    props: ['value', 'atomCollection', 'molecule', 'moleculeid'],
    data() {
        return {
          firstSelectedId: 0,
          secondSelectedId: 0,
          thirdSelectedId: 0,
          fourthSelectedId: 0,

          //
          currentRotateX: 0,
          currentRotateY: 0,
          currentRotateZ: 0,
          currentWidth: "20%",
          currentHeight: "20%",
          currentOpacity:"1",

          //
          nukleolus: true,
          selected: "",


          //selection
          isSelectedFirst: false,
          isSelectedSecond: false,
          isSelectedThird: false,
          isSelectedFourth: false,

          //delay
          sizeDelay: 0,
          rotationDelay: 0,
          opacityDelay: 0
        }
    },
    mounted: function() {
      this.nukleolus = false
    },
    computed: {
      id(){
        return this.moleculeid
      },
      atoms(){
        return this.atomCollection.sort(function (a, b) {
          if (a.atomid > b.atomid) {
            return 1
          }
          if (a.atomid < b.atomid) {
            return -1
          }
          // a must be equal to b
          0
        })
      },

      firstSelected(){
        let id = this.firstSelectedId
        return !id ? null : this.atomCollection.find(atom => atom.atomid === id),
        this.atomCollection[id]


      },
      secondSelected(){
        let id = this.secondSelectedId
        return !id ? null : this.atomCollection.find(atom => atom.atomid === id),
        this.atomCollection[id]
      },
      thirdSelected(){
        let id = this.thirdSelectedId
        return !id ? null : this.atomCollection.find(atom => atom.atomid === id),
        this.atomCollection[id]
      },


    },

    methods: {

        //before animation
        beforeEnter: function(el) {
            el.style.width = this.firstSelected.widthstart + "%",
            el.style.height = this.firstSelected.heightstart + "%",
            el.style.transform = "rotateX("+ this.secondSelected.rotationxstart +"deg)",
            el.style.transform = "rotateY("+ this.secondSelected.rotationystart  +"deg)",
            el.style.transform = "rotateZ("+ this.secondSelected.rotationzstart  +"deg)",
            el.style.opacity = this.thirdSelected.opacitystart / 100

        },

        //animation enter
        enter: function(el, done) {
            var vm = this
            Velocity(el, {
              width: this.firstSelected.widthfinal + "%",
              height: this.firstSelected.heightfinal + "%"

            }, {
                delay: 2000 + +this.sizeDelay,
                easing: this.firstSelected.spacing,
                duration: this.firstSelected.timing,
                complete: function() {
                   done()
                   if (!vm.stop) vm.nukleolus = false
                }
            })
            Velocity(el, {

              rotateX: this.secondSelected.rotationxfinal + "deg",
              rotateY: this.secondSelected.rotationyfinal + "deg",
              rotateZ: this.secondSelected.rotationzfinal + "deg"
            }, {
                delay: 2000 + +this.rotationDelay,
                easing: this.secondSelected.spacing,
                duration: this.secondSelected.timing,
                queue: false,
                complete: function() {
                   done()
                   if (!vm.stop) vm.nukleolus = false
                }
            })
            Velocity(el, {
              opacity: this.thirdSelected.opacityfinal / 100,
            }, {
                delay: 2000 + +this.opacityDelay,
                easing: this.thirdSelected.spacing,
                duration: this.thirdSelected.timing,
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
