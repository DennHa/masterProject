<template name="showcase">
<div class="showcase__bond">

    <div class="molecule__viewer">
      <div class="molecule__nukleolusWrapper">
        <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
            <div class="molecule__nukleolus" v-if="nukleolus"></div>
        </transition>
      </div>

    </div>
    <div class="showcase__properties">
      <h2 v-if="selected == '-'">Example </h2>
      <h2 v-if="scaleIt >= 1">{{scaleSelected.name}} </h2>
      <h2 v-if="translateIt >= 1">{{translateSelected.name}}</h2>
      <h2 v-if="rotationIt >= 1 == 'rotation'">{{rotationSelected.name}}</h2>
      <h2 v-if="opacityIt >= 1">{{opacitySelected.name}}</h2>
      <div>
        <select  class="atom__kind" v-model="selected">
           <option  v-for="chooseThis in choose" >
             {{ chooseThis.name }}
           </option>
        </select>
        <br>
        <select  class="atom__kind"  v-model="scaleIt"  v-if="selected == 'scale'">
          <option v-if="atom.widthfinal >= 0" v-for="atom in atoms" :value="atom.atomid">
            {{ atom.name }}
          </option>
        </select>

        <select  class="atom__kind" v-model="translateIt" v-if="selected == 'translate'">
           <option v-if="atom.translate >= 0" v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>

        <select  class="atom__kind" v-model="rotationIt" v-if="selected == 'rotation'">
           <option v-if="atom.rotationzfinal >= 0" v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>
        <select  class="atom__kind" v-model="opacityIt" v-if="selected == 'opacity'">
           <option v-if="atom.opacityfinal >= 0" v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>

    </div>


</template>
<script>


export default {
    name: "showcase",

    props: ['', 'atomcollection', 'showcase', 'thismoleculeid', 'globalDelay'],
    data() {
        return {
          scaleIt: 0,
          translateIt: 0,
          rotationIt: 0,
          opacityIt: 0,
          copied: false,
          scaleSelectedId: 0,
          rotationSelectedId: 0,
          opacitySelectedId: 0,
          fourthSelectedId: 0,
          choose: [
            {name: "-"},
            {name: "scale"},
            {name: "translate"},
            {name: "rotation"},
            {name: "opacity"},

          ],

          //
          nukleolus: true,
          selected: "-",
        }
    },
    mounted: function() {
      this.nukleolus = false
    },
    computed: {

      id(){
        return 0  //weil wir "-" als erstes molekül haben
      },

      atoms(){
        return this.atomcollection.sort(function (a, b) {
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

      scaleSelected(){
        let d = this.showcase[this.id].scaleId
        return !d ? null : this.atomcollection.find(atom => atom.atomid === d),
        this.atomcollection[this.scaleIt]

      },
      rotationSelected(){
        let d = this.showcase[this.id].rotationId
        return !d ? null : this.atomcollection.find(atom => atom.atomid === d),
        this.atomcollection[this.rotationIt]
      },
      opacitySelected(){
        let d = this.showcase[this.id].opacityId
        return !d ? null : this.atomcollection.find(atom => atom.atomid === d),
        this.atomcollection[this.opacityIt]
      },
      translateSelected(){
        let d = this.showcase[this.id].translateId
        return !d ? null : this.atomcollection.find(atom => atom.atomid === d),
        this.atomcollection[this.translateIt]
      },

      translateSelectedId(){
        return this.translateSelected.atomid
      },
      rotationSelectedId(){
        return this.rotationSelected.atomid
      }

      //atoms


    },

    methods: {
      copyThis(){
        var clipboard = new Clipboard('#' + this.showcase[this.id].name + this.showcase[this.id].molid)
        this.copied = true
        var self = this
          setTimeout(function(){
              self.copied = false;
          }, 1000);
      },
        //before animation
        beforeEnter: function(el) {
            el.style.width = +this.scaleSelected.widthstart * this.showcase[this.id].viewPortScaleX + "px",
            el.style.height = +this.scaleSelected.heightstart * this.showcase[this.id].viewPortScaleY + "px",
            el.style.transform = "rotateX("+ this.rotationSelected.rotationxstart +"deg)",
            el.style.transform = "rotateY("+ this.rotationSelected.rotationystart  +"deg)",
            el.style.transform = "rotateZ("+ this.rotationSelected.rotationzstart  +"deg)"
            if(this.translateSelected.translate){el.style.opacity = 0}

            Velocity(el, {
                opacity: this.opacitySelected.opacitystart / 100,
                width: +this.scaleSelected.widthstart * this.showcase[this.id].viewPortScaleX + "px",
                height: +this.scaleSelected.heightstart * this.showcase[this.id].viewPortScaleY + "px",
                rotateX: this.rotationSelected.rotationxstart,
                rotateY: this.rotationSelected.rotationystart,
                rotateZ: this.rotationSelected.rotationzstart,
                translateX: +this.translateSelected.translateXstart   *  this.showcase[this.id].viewPortScaleX - 180 *  this.showcase[this.id].viewPortScaleX + "px",
                translateY: +this.translateSelected.translateYstart *  this.showcase[this.id].viewPortScaleY - 320 *  this.showcase[this.id].viewPortScaleY + "px"
            }, {
                duration: 0,
                delay: "0",
                queue: false

            })

        },

        //animation enter
        enter: function(el, done) {
            var vm = this


            // console.log(test))
            Velocity(el, {
              width: +this.scaleSelected.widthfinal * this.showcase[this.id].viewPortScaleX + "px",
              height: +this.scaleSelected.heightfinal * this.showcase[this.id].viewPortScaleY + "px"

            }, {
                delay: this.globalDelay + +this.showcase[this.id].scaleDelay,
                easing: this.translateSelected.spacing,
                duration: this.translateSelected.timing,
                complete: function() {
                   done()
                   if (!vm.stop) vm.nukleolus = false
                }
            })
            Velocity(el, {
              rotateX: this.rotationSelected.rotationxfinal + "deg",
              rotateY: this.rotationSelected.rotationyfinal + "deg",
              rotateZ: this.rotationSelected.rotationzfinal + "deg"
            }, {
                delay: this.globalDelay ,
                easing: this.rotationSelected.spacing,
                duration: this.rotationSelected.timing,
                queue: false,
                complete: function() {
                   done()
                   if (!vm.stop) vm.nukleolus = false
                }
            })
            Velocity(el, {
              opacity: this.opacitySelected.opacityfinal / 100,
            }, {
                delay: this.globalDelay ,
                easing: this.opacitySelected.spacing,
                duration: this.opacitySelected.timing,
                queue: false,
                complete: function() {
                   done()
                   if (!vm.stop) vm.nukleolus = false
                }
            })

              Velocity(el, {
                translateX:  +this.translateSelected.translateXfinal *  this.showcase[this.id].viewPortScaleX - 180 *  this.showcase[this.id].viewPortScaleX + "px",
                translateY: +this.translateSelected.translateYfinal *  this.showcase[this.id].viewPortScaleY - 320 *  this.showcase[this.id].viewPortScaleY + "px"
              }, {
                  delay: this.globalDelay,
                  easing: this.translateSelected.spacing,
                  duration: this.translateSelected.timing,
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
                backgroundColor: 'transparent',
            }, {
                duration: 0,
                delay: this.globalDelay,
                complete: function() {
                    done()
                    vm.nukleolus = true
                }
            })
        }
    },

}

</script>
