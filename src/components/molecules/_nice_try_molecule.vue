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
           <option v-for="atomsize in atomSize" :value="atomsize.id">
             {{ atomsize.name }}
           </option>
        </select>
        </select>
        <select  class="atom__kind" v-model="secondSelectedId">
           <option v-for="atomrotation in atomRotation" :value="atomrotation.id">
             {{ atomrotation.name }}
           </option>
        </select>
        <select  class="atom__kind" v-model="thirdSelectedId">
           <option v-for="atomopacity in atomOpacity" :value="atomopacity.id">
             {{ atomopacity.name }}
           </option>
        </select>
    </div>


        <div class="molecule__timing">
          <!-- <label for="firstDelay">first delay</label>
          <input type="checkbox" id="firstDelay" value="firstDelay" v-model="checkedDelays"><br> -->



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

    props: ['atomSize', 'atomRotation', 'atomOpacity'],
    data() {
        return {
          firstSelectedId: 0,
          secondSelectedId: 0,
          thirdSelectedId: 0,

          nukleolus: true,
          selected: "",
          value: "",


        }
    },
    mounted: function() {
      this.nukleolus = false
    },

    computed: {
      firstSelected(){
        let id = this.firstSelectedId
        if (id) {
          return this.atomSize.find(atom => atom.id === id)
        }
        return this.atomSize[this.firstSelectedId]
      },
      secondSelected(){
        let id = this.firstSecondId
        if (id) {
          return this.atomRotation.find(atom => atom.id === id)
        }
        return this.atomRotation[this.secondSelectedId]
      },
      thirdSelected(){
        let id = this.firstThirdId
        if (id) {
          return this.atomOpacity.find(atom => atom.id === id)
        }
        return this.atomOpacity[this.thirdSelectedId]
      },

      //
      newAtomSize(){
        return this.atomSize.concat([{name: "-", id: 0, width:"20", height:"20" }],  this.atomSize)
      }

    },

    methods: {

        //before animation
        beforeEnter: function(el) {
            const thisSize = this.atomSize[this.firstSelectedId]
            const thisRotation = this.atomRotation[this.secondSelectedId]
            const thisOpacity = this.atomOpacity[this.thirdSelectedId]
            el.style.width = thisSize.widthstart + "%",
            el.style.height = thisSize.heightstart + "%",
            el.style.transform = "rotateX("+ thisRotation.rotationxstart +"deg)",
            el.style.transform = "rotateY("+ thisRotation.rotationystart  +"deg)",
            el.style.transform = "rotateZ("+ thisRotation.rotationzstart  +"deg)",
            el.style.opacity = thisOpacity.opacitystart / 100

        },

        //animation enter
        enter: function(el, done) {
            const thisSize = this.atomSize[this.firstSelectedId]
            const thisRotation = this.atomRotation[this.secondSelectedId]
            const thisOpacity = this.atomOpacity[this.thirdSelectedId]
            var vm = this
            Velocity(el, {

             rotateX: thisRotation.rotationxfinal + "deg",
              rotateY: thisRotation.rotationyfinal + "deg",
              rotateZ: thisRotation.rotationzfinal + "deg",
              width: thisSize.widthfinal + "%",
              height: thisSize.heightfinal + "%",
              opacity: thisOpacity.opacityfinal / 100
            }, {
                delay: "2000",
                easing: thisSize.spacing,
                duration: thisSize.timing,

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
