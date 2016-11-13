<template name="molecule">
<div class="molecule__bond">

    <div class="molecule__viewer">
        <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
            <div class="molecule__nukleolus" v-if="nukleolus"></div>
        </transition>
    </div>
    <div class="molecule__properties">
      <form class="" action="index.html" method="post">
        <input name="name" class="atom__name">
      </form>
      <div>
        <select  class="atom__kind" v-model="firstSelectedId">
           <option v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>
        </select>
        <select  class="atom__kind" v-model="secondSelectedId">
           <option v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>
        <select  class="atom__kind" v-model="thirdSelectedId">
           <option v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>
        <select  class="atom__kind" v-model="fourthSelectedId">
           <option v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>
    </div>


        <div class="molecule__timing">
          <!-- <label for="firstDelay">first delay</label>
          <input type="checkbox" id="firstDelay" value="firstDelay" v-model="checkedDelays"><br> -->
          <label for="secondDelay"> second delay</label>
          <input type="checkbox" id="secondDelay" value="secondDelay" v-model="isSelectedSecond"><br>
          <label for="thirdDelay">third delay</label>
          <input type="checkbox" id="thirdDelay" value="thirdDelay" v-model="isSelectedThird"><br>
          <label for="fourthDelay">fourth delay</label>
          <input type="checkbox" id="fourthDelay" value="fourthDelay" v-model="isSelectedFourth">


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
    name: "molecule",

    props: ['atomCollection'],
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
          value: "",

          //selection
          isSelectedFirst: false,
          isSelectedSecond: false,
          isSelectedThird: false,
          isSelectedFourth: false
        }
    },
    mounted: function() {
      this.nukleolus = false
    },
    updated(){

    },
    computed: {
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
        if (id) {
          return this.atomCollection.find(atom => atom.atomid === id)
        }
        return "hey"
      },
      secondSelected(){
        let id = this.secondSelectedId
        return !id ? null : this.atomCollection.find(atom => atom.atomid === id),
        ""
      },
      thirdSelected(){
        let id = this.thirdSelectedId
        return !id ? null : this.atomCollection.find(atom => atom.atomid === id),
        ""
      },
      fourthSelected(){
        let id = this.fourthSelectedId
        return !id ? null : this.atomCollection.find(atom => atom.atomid === id),
        ""
      },

      // queue
      isQueueSecond(){
        if (this.isSelectedSecond) {
          return null
        }
        return false
      },
      isQueueThird(){
        if (this.isSelectedSecond) {
          return null
        }
        return false
      },
      isQueueFourth(){
        if (this.isSelectedSecond) {
          return null
        }
        return false
      }


    },

    methods: {

        //before animation
        beforeEnter: function(el) {
          const firstSel = this.atomCollection[this.firstSelectedId]
            el.style.width = firstSel.widthstart + "%",
            el.style.height = firstSel.heightstart + "%",
            el.style.transform = "rotateX("+ firstSel.rotationxstart +"deg)",
            el.style.transform = "rotateY("+ firstSel.rotationystart  +"deg)",
            el.style.transform = "rotateZ("+ firstSel.rotationzstart  +"deg)",
            el.style.opacity = firstSel.opacitystart / 100

        },

        //animation enter
        enter: function(el, done) {
            var vm = this
            const firstSel = this.atomCollection[this.firstSelectedId]
            const secondSel = this.atomCollection[this.secondSelectedId]
            const thirdSel = this.atomCollection[this.thirdSelectedId]
            const fourthSel = this.atomCollection[this.fourthSelectedId]

            Velocity(el, {
              rotateX(){
                vm.currentRotateX = !firstSel.rotationxfinal ? "0" : firstSel.rotationxfinal + "deg"
                return vm.currentRotateX

              },
              rotateY(){
                vm.currentRotateY = !firstSel.rotationyfinal ? "0" : firstSel.rotationyfinal + "deg"
                return vm.currentRotateY

              },
              rotateZ(){
                 vm.currentRotateZ = !firstSel.rotationzfinal ? "0" : firstSel.rotationzfinal + "deg"
                 return vm.currentRotateZ
              },
              width(){
                vm.currentWidth = !firstSel.widthfinal ? "20%" : firstSel.widthfinal + "%"
                return vm.currentWidth
              },
              height(){
                vm.currentHeight = !firstSel.heightfinal ? "20%" : firstSel.heightfinal + "%"
                return vm.currentHeight
              },
              opacity(){
                vm.currentOpacity = !firstSel.opacityfinal ? "1" : firstSel.opacityfinal / 100
                return vm.currentOpacity

               }
            }, {
                delay: "2000",
                easing: firstSel.spacing,
                duration: firstSel.timing,
                complete: function() {
                    done()
                    if (!vm.stop) vm.nukleolus = false
                }
            })

            Velocity(el, {
              rotateX(){
                vm.currentRotateX = !secondSel.rotationxfinal ? vm.currentRotateX : secondSel.rotationxfinal - secondSel.rotationxstart
                return vm.currentRotateX

              },
              rotateY(){
                vm.currentRotateY = !secondSel.rotationyfinal ? vm.currentRotateY : secondSel.rotationyfinal - secondSel.rotationystart
                return vm.currentRotateY

              },
              rotateZ(){
                 vm.currentRotateZ = !secondSel.rotationzfinal ? vm.currentRotateZ : secondSel.rotationzfinal - secondSel.rotationzstart
                 return vm.currentRotateZ
              },
              width(){
                vm.currentWidth = !secondSel.widthfinal ? vm.currentWidth : secondSel.widthfinal - secondSel.widthstart
                return vm.currentWidth
              },
              height(){
                vm.currentHeight = !secondSel.heightfinal ? vm.currentHeight : secondSel.heightfinal - secondSel.heightstart
                return vm.currentHeight
              },
              opacity(){
                vm.currentOpacity = !firstSel.opacityfinal ? "1" : firstSel.opacityfinal / 100
                return vm.currentOpacity

               }
            }, {
                delay: "2000",
                easing: firstSel.spacing,
                duration: firstSel.timing,
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
