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


        </div>
        <div class="subMenu">
          <div class="subMenu__copied" v-show="copied">copied</div>
          <div v-bind:id="value[id].name + value[id].molid " v-on:click="copyThis" v-bind:data-clipboard-target="'.' + copyThisValue"></div>

        </div>

        <div v-bind:class="copyThisValue" class="copy">
          //css Animation Specs - {{value[id].name}}  <br>
          .{{value[id].name}} { <br>
          &nbsp;  &nbsp;  animation: {{value[id].name}}_scale {{firstSelected.timing}}ms {{firstSelected.spacing}} {{value[id].scaleDelay}};<br>
          &nbsp;  &nbsp;  animation: {{value[id].name}}_rotation {{secondSelected.timing}}ms {{secondSelected.spacing}} {{value[id].rotationDelay}};<br>
          &nbsp;  &nbsp;  animation: {{value[id].name}}_opacity {{thirdSelected.timing}}ms {{thirdSelected.spacing}} {{value[id].opacityDelay}};<br>
          &nbsp;  }<br>
          &nbsp;  <br>
          &nbsp;  @keyframes {{value[id].name}}_scale {<br>
          &nbsp;  &nbsp;  0% {<br>
          &nbsp; &nbsp;  width: {{firstSelected.widthstart}}px; //in pixel!<br>
          &nbsp; &nbsp;  height: {{firstSelected.heightstart}}px; //in pixel!<br>
          &nbsp;  }<br>
          &nbsp;  100% {<br>
          &nbsp; &nbsp;  width: {{firstSelected.widthfinal}}px; //in pixel!<br>
          &nbsp; &nbsp;  height: {{firstSelected.heightfinal}}px; //in pixel!<br>
          &nbsp;  }<br>
          &nbsp;  @keyframes {{value[id].name}}_rotation {<br>
          &nbsp;  &nbsp;  0% {<br>
          &nbsp;  &nbsp;  transform: rotatX({{secondSelected.rotationxstart}});<br>
          &nbsp;  &nbsp;  transform: rotatY({{secondSelected.rotationystart}});<br>
          &nbsp;  &nbsp;  transform: rotatZ({{secondSelected.rotationzstart}});<br>
          &nbsp;  }<br>
          &nbsp;  100% {<br>
          &nbsp;  &nbsp;  transform: rotatX({{secondSelected.rotationxfinal}});<br>
          &nbsp;  &nbsp;  transform: rotatY({{secondSelected.rotationyfinal}});<br>
          &nbsp; &nbsp;  transform: rotatZ({{secondSelected.rotationzfinal}});<br>
          &nbsp;  }<br>
          &nbsp;  @keyframes {{value[id].name}}_opacity {<br>
          &nbsp;  &nbsp;  0% {<br>
          &nbsp; &nbsp;  opacity: {{thirdSelected.opacitystart / 100}};<br>
          &nbsp;  }<br>
          &nbsp;  100% {<br>
          &nbsp; &nbsp;  opacity: {{thirdSelected.opacityfinal / 100 }}; <br>
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
          firstSelectedId: 0,
          secondSelectedId: 0,
          thirdSelectedId: 0,
          fourthSelectedId: 0,


          //
          nukleolus: true,
          selected: "",


          //selection
          isSelectedFirst: false,
          isSelectedSecond: false,
          isSelectedThird: false,
          isSelectedFourth: false,
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

      firstSelected(){
        let d = this.value[this.id].scaleId
        return !d ? null : this.atomCollection.find(atom => atom.atomid === d),
        this.atomCollection[d]

      },
      secondSelected(){
        let d = this.value[this.id].rotationId
        return !d ? null : this.atomCollection.find(atom => atom.atomid === d),
        this.atomCollection[d]
      },
      thirdSelected(){
        let d = this.value[this.id].opacityId
        return !d ? null : this.atomCollection.find(atom => atom.atomid === d),
        this.atomCollection[d]
      },


    },

    methods: {
      copyThis(){
        var clipboard = new Clipboard('#' + this.value[this.id].name + this.value[this.id].molid)
      },
        //before animation
        beforeEnter: function(el) {
            el.style.width = this.firstSelected.widthstart * this.value[this.id].viewPortScaleX  + "px",
            el.style.height = this.firstSelected.heightstart * this.value[this.id].viewPortScaleY + "px",
            el.style.transform = "rotateX("+ this.secondSelected.rotationxstart +"deg)",
            el.style.transform = "rotateY("+ this.secondSelected.rotationystart  +"deg)",
            el.style.transform = "rotateZ("+ this.secondSelected.rotationzstart  +"deg)",
            el.style.opacity = this.thirdSelected.opacitystart / 100,
            Velocity(el, {
                rotateX: this.secondSelected.rotationxstart,
                rotateY: this.secondSelected.rotationystart,
                rotateZ: this.secondSelected.rotationzstart
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
              width: +this.firstSelected.widthfinal * this.value[this.id].viewPortScaleX + "px",
              height: +this.firstSelected.heightfinal * this.value[this.id].viewPortScaleY +   "px"

            }, {
                delay: 2000 + +this.value[this.id].scaleDelay,
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
                delay: 2000 + +this.value[this.id].rotationDelay,
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
                delay: 2000 + +this.value[this.id].opacityDelay,
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
