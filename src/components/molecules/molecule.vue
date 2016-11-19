<template name="molecule">
<div class="molecule__bond">

    <div class="molecule__viewer">
      <div class="molecule__nukleolusWrapper">
        <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
            <div class="molecule__nukleolus" v-if="nukleolus"></div>
        </transition>
      </div>

    </div>
    <div class="molecule__properties">
      <h3>molecule</h3>
      <form class="" action="index.html" method="post">
        <input name="name" class="atom__name" v-model="value[id].name" >
      </form>
      <div>
        <select  class="atom__kind" v-model="value[id].scaleId">
           <option v-if="atom.widthfinal >= 0" v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>
        <span class="connectedIt">&</span>
        <select  class="atom__kind" v-model="value[id].translateId">
           <option v-if="atom.translateYfinal >= 0" v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>
        <span class="connectedIt">&</span>
        <select  class="atom__kind" v-model="value[id].rotationId">
           <option v-if="atom.rotationzfinal >= 0" v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>
        <span class="connectedIt">&</span>
        <select  class="atom__kind" v-model="value[id].opacityId">
           <option v-if="atom.opacityfinal >= 0" v-for="atom in atoms" :value="atom.atomid">
             {{ atom.name }}
           </option>
        </select>

    </div>
    <span class="warning" v-if="translateSelectedId >= 1 && rotationSelectedId >= 1">Combining translation & rotation doesn't work yet</span>

        <div class="molecule__timing">

          <div class="molecule__scaleDelay" v-if="value[id].scaleId >= 1">
            <h3>scale delay {{value[id].scaleDelay}}</h3>
            <input type="range" v-model="value[id].scaleDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
          <div class="molecules__rotationDelay" v-if="value[id].rotationId >= 1">
            <h3>rotation delay {{value[id].rotationDelay}}</h3>
            <input type="range" v-model="value[id].rotationDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
          <div class="molecules__opacityDelay" v-if="value[id].opacityId >= 1">
            <h3>opacity delay {{value[id].opacityDelay}}</h3>
            <input  type="range" v-model="value[id].opacityDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
          <div class="molecules__opacityDelay" v-if="value[id].translateId >= 1">
            <h3>translate delay {{value[id].translateDelay}}</h3>
            <input  type="range" v-model="value[id].translateDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>


        </div>
        <div class="subMenu">
          <transition name="fade">
            <div class="subMenu__copied" v-show="copied">copied</div>
          </transition>
          <div v-bind:id="value[id].name + value[id].molid " v-on:click="copyThis" v-bind:data-clipboard-target="'.' + copyThisValue"></div>

        </div>

        <div v-bind:class="copyThisValue" class="copy">
          //css Animation Specs - {{value[id].name}}  <br>
          .{{value[id].name}} { <br>
          &nbsp;  &nbsp;  animation: {{value[id].name}}_scale {{scaleSelected.timing}}ms {{scaleSelected.spacing}} {{value[id].scaleDelay}};<br>
          &nbsp;  &nbsp;  animation: {{value[id].name}}_rotation {{rotationSelected.timing}}ms {{rotationSelected.spacing}} {{value[id].rotationDelay}};<br>
          &nbsp;  &nbsp;  animation: {{value[id].name}}_opacity {{opacitySelected.timing}}ms {{opacitySelected.spacing}} {{value[id].opacityDelay}};<br>
          &nbsp;  &nbsp;  animation: {{value[id].name}}_translate {{opacitySelected.timing}}ms {{opacitySelected.spacing}} {{value[id].opacityDelay}};<br>
          &nbsp;  }<br>
          &nbsp;  <br>
          &nbsp;  @keyframes {{value[id].name}}_scale {<br>
          &nbsp;  &nbsp;  0% {<br>
          &nbsp; &nbsp;  width: {{scaleSelected.widthstart}}px; //in pixel!<br>
          &nbsp; &nbsp;  height: {{scaleSelected.heightstart}}px; //in pixel!<br>
          &nbsp;  }<br>
          &nbsp;  100% {<br>
          &nbsp; &nbsp;  width: {{scaleSelected.widthfinal}}px; //in pixel!<br>
          &nbsp; &nbsp;  height: {{scaleSelected.heightfinal}}px; //in pixel!<br>
          &nbsp;  }<br>
          &nbsp;  @keyframes {{value[id].name}}_rotation {<br>
          &nbsp;  &nbsp;  0% {<br>
          &nbsp;  &nbsp;  transform: rotatX({{rotationSelected.rotationxstart}});<br>
          &nbsp;  &nbsp;  transform: rotatY({{rotationSelected.rotationystart}});<br>
          &nbsp;  &nbsp;  transform: rotatZ({{rotationSelected.rotationzstart}});<br>
          &nbsp;  }<br>
          &nbsp;  100% {<br>
          &nbsp;  &nbsp;  transform: rotatX({{rotationSelected.rotationxfinal}});<br>
          &nbsp;  &nbsp;  transform: rotatY({{rotationSelected.rotationyfinal}});<br>
          &nbsp; &nbsp;  transform: rotatZ({{rotationSelected.rotationzfinal}});<br>
          &nbsp;  }<br>
          &nbsp;  @keyframes {{value[id].name}}_opacity {<br>
          &nbsp;  &nbsp;  0% {<br>
          &nbsp; &nbsp;  opacity: {{opacitySelected.opacitystart / 100}};<br>
          &nbsp;  }<br>
          &nbsp;  100% {<br>
          &nbsp; &nbsp;  opacity: {{opacitySelected.opacityfinal / 100 }}; <br>
          &nbsp;  }<br>

          &nbsp;  @keyframes {{value[id].name}}_translate {<br>
          &nbsp;  &nbsp;  0% {<br>
          &nbsp; &nbsp;  transform: translate({{translateSelected.translateXstart}}px  {{translateSelected.translateYstart}}px); //in pixel!<br>
          &nbsp;  }<br>
          &nbsp;  100% {<br>
          &nbsp; &nbsp;  transform: translate({{translateSelected.translateXfinal}}px  {{translateSelected.translateYfinal}}px); //in pixel!<br>
          &nbsp;  }<br>
          }
        </div>
</div>
</template>
<script>


export default {
    name: "molecules",

    props: ['value', 'atomCollection', 'molecule', 'moleculeid'],
    data() {
        return {
          copied: false,
          scaleSelectedId: 0,
          rotationSelectedId: 0,
          opacitySelectedId: 0,
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
        return this.moleculeid  //weil wir "-" als erstes molekül haben
      },
      copyThisValue(){
          return   this.value[this.id].name + this.value[this.id].molid + "_id"
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

      scaleSelected(){
        let d = this.value[this.id].scaleId
        return !d ? null : this.atomCollection.find(atom => atom.atomid === d),
        this.atomCollection[d]

      },
      rotationSelected(){
        let d = this.value[this.id].rotationId
        return !d ? null : this.atomCollection.find(atom => atom.atomid === d),
        this.atomCollection[d]
      },
      opacitySelected(){
        let d = this.value[this.id].opacityId
        return !d ? null : this.atomCollection.find(atom => atom.atomid === d),
        this.atomCollection[d]
      },
      translateSelected(){
        let d = this.value[this.id].translateId
        return !d ? null : this.atomCollection.find(atom => atom.atomid === d),
        this.atomCollection[d]
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
        var clipboard = new Clipboard('#' + this.value[this.id].name + this.value[this.id].molid)
        this.copied = true
        var self = this
          setTimeout(function(){
              self.copied = false;
          }, 1000);
      },
        //before animation
        beforeEnter: function(el) {
            el.style.width = +this.scaleSelected.widthstart * this.value[this.id].viewPortScaleX + "px",
            el.style.height = +this.scaleSelected.heightstart * this.value[this.id].viewPortScaleY + "px",
            el.style.transform = "rotateX("+ this.rotationSelected.rotationxstart +"deg)",
            el.style.transform = "rotateY("+ this.rotationSelected.rotationystart  +"deg)",
            el.style.transform = "rotateZ("+ this.rotationSelected.rotationzstart  +"deg)",
            el.style.opacity = 0, //gegen das flackern
            Velocity(el, {
                opacity: this.opacitySelected.opacitystart / 100,
                width: +this.scaleSelected.widthstart * this.value[this.id].viewPortScaleX + "px",
                height: +this.scaleSelected.heightstart * this.value[this.id].viewPortScaleY + "px",
                rotateX: this.rotationSelected.rotationxstart,
                rotateY: this.rotationSelected.rotationystart,
                rotateZ: this.rotationSelected.rotationzstart,
                translateX: +this.translateSelected.translateXstart   *  this.value[this.id].viewPortScaleX - 180 *  this.value[this.id].viewPortScaleX + "px",
                translateY: +this.translateSelected.translateYstart *  this.value[this.id].viewPortScaleY - 320 *  this.value[this.id].viewPortScaleY + "px"
            }, {
                duration: 0,
                delay: "0",
                queue: false

            })

        },

        //animation enter
        enter: function(el, done) {
            var vm = this

            console.log(+this.translateSelected.translateXfinal *  this.value[this.id].viewPortScaleY )
            // console.log(test))
            Velocity(el, {
              width: +this.scaleSelected.widthfinal * this.value[this.id].viewPortScaleX + "px",
              height: +this.scaleSelected.heightfinal * this.value[this.id].viewPortScaleY + "px"

            }, {
                delay: 2000 + +this.value[this.id].scaleDelay,
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
                delay: 2000 + +this.value[this.id].rotationDelay,
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
                delay: 2000 + +this.value[this.id].opacityDelay,
                easing: this.opacitySelected.spacing,
                duration: this.opacitySelected.timing,
                queue: false,
                complete: function() {
                   done()
                   if (!vm.stop) vm.nukleolus = false
                }
            })

              Velocity(el, {

                // let test = +this.translateSelected.translateXfinal *  this.value[this.id].viewPortScaleY  - 320 *  this.value[this.id].viewPortScaleY
                // console.log(test)
                translateX: +this.translateSelected.translateXfinal *  this.value[this.id].viewPortScaleX + "px",
                translateY: +this.translateSelected.translateXfinal *  this.value[this.id].viewPortScaleY  + "px"
              }, {
                  delay: 2000 + +this.value[this.id].translateDelay,
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
