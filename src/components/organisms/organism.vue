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
        <span class="connectedIt" v-if="value[id].firstMoleculeId >= 1">+</span>
        <select  class="organism__kind" v-model="value[id].secondMoleculeId" v-if="value[id].firstMoleculeId >= 1">
           <option v-for="molecule in moleculeCollection" :value="molecule.molid">
             {{ molecule.name }}
           </option>
        </select>

    </div>
    <span class="advice">Your first selected molecule's final values need to match your second selected molecule's start values </span>


        <div class="organism__timing">

          <div class="organism__scaleDelay" v-if="this.firstSelectedscaleId >= 1 || this.firstSelectedRotationId >= 1 || this.firstSelectedOpacityId >= 1 || this.firstSelectedTranslateId >= 1">
            <h3>first delay {{value[id].firstDelay}}</h3>
            <input type="range" v-model="value[id].firstDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
        </div>
        <div class="organism__timing">
          <div class="organism__rotationDelay" v-if="this.secondSelectedscaleId >= 1 || this.secondSelectedRotationId >= 1 || this.secondSelectedOpacityId >= 1 || this.secondSelectedTranslateId >= 1">
            <h3>second delay {{value[id].secondDelay}}</h3>
            <input type="range" v-model="value[id].secondDelay" min="0" max="1000" step="10" defaultValue="0">
          </div>
        </div>
        <div class="subMenu">
          <transition name="fade">
            <div class="subMenu__copied" v-show="copied">copied</div>
          </transition>
              <div v-bind:id="value[id].name + value[id].orgid " v-on:click="copyThis" v-bind:data-clipboard-target="'.' + copyThisValue"></div>

            </div>

            <div v-bind:class="copyThisValue" class="copy">
              //css Animation Specs - {{value[id].name}}  <br>
              .{{value[id].name}} { <br>
              &nbsp;  &nbsp;  animation: {{value[id].name}}_scale_one {{atomCollection[firstSelectedscaleId].timing}}ms  {{atomCollection[firstSelectedscaleId].spacing}} {{+firstSelected.scaleDelay +
               +value[id].firstDelay}};<br>
              &nbsp;  &nbsp;  animation: {{value[id].name}}_rotation_one {{atomCollection[firstSelectedRotationId].timing}}ms  {{atomCollection[firstSelectedRotationId].spacing}} {{+firstSelected.rotationDelay +
               +value[id].firstDelay}};<br>
              &nbsp;  &nbsp;  animation: {{value[id].name}}_opacity_one {{atomCollection[firstSelectedOpacityId].timing}}ms  {{atomCollection[firstSelectedOpacityId].spacing}} {{+firstSelected.opacityDelay +
               +value[id].firstDelay}};<br>
              &nbsp;  &nbsp;  animation: {{value[id].name}}_scale_second {{atomCollection[secondSelectedscaleId].timing}}ms  {{atomCollection[secondSelectedscaleId].spacing}} {{+secondSelected.scaleDelay +
               +value[id].secondDelay}};<br>
              &nbsp;  &nbsp;  animation: {{value[id].name}}_rotation_second {{atomCollection[secondSelectedRotationId].timing}}ms  {{atomCollection[secondSelectedRotationId].spacing}} {{+secondSelected.rotationDelay +
               +value[id].secondDelay}};<br>
              &nbsp;  &nbsp;  animation: {{value[id].name}}_opacity_second {{atomCollection[secondSelectedOpacityId].timing}}ms  {{atomCollection[secondSelectedOpacityId].spacing}} {{+secondSelected.opacityDelay +
               +value[id].secondDelay}};<br>
              &nbsp;  }<br>
              &nbsp;  <br>
              &nbsp;  @keyframes {{value[id].name}}_scale_one {<br>
              &nbsp;  &nbsp;  0% {<br>
              &nbsp; &nbsp;  width: {{atomCollection[firstSelectedscaleId].widthstart}}px; //in pixel!<br>
              &nbsp; &nbsp;  height: {{atomCollection[firstSelectedscaleId].heightstart}}px; //in pixel!<br>
              &nbsp;  }<br>
              &nbsp;  100% {<br>
              &nbsp; &nbsp;  width: {{atomCollection[firstSelectedscaleId].widthfinal}}px; //in pixel!<br>
              &nbsp; &nbsp;  height: {{atomCollection[firstSelectedscaleId].heightfinal}}px; //in pixel!<br>
              &nbsp;  }<br>
              &nbsp;  @keyframes {{value[id].name}}_rotation_one {<br>
              &nbsp;  &nbsp;  0% {<br>
              &nbsp;  &nbsp;  transform: rotatX({{atomCollection[firstSelectedRotationId].rotationxstart}});<br>
              &nbsp;  &nbsp;  transform: rotatY({{atomCollection[firstSelectedRotationId].rotationystart}});<br>
              &nbsp;  &nbsp;  transform: rotatZ({{atomCollection[firstSelectedRotationId].rotationzstart}});<br>
              &nbsp;  }<br>
              &nbsp;  100% {<br>
              &nbsp;  &nbsp;  transform: rotatX({{atomCollection[firstSelectedRotationId].rotationxfinal}});<br>
              &nbsp;  &nbsp;  transform: rotatY({{atomCollection[firstSelectedRotationId].rotationyfinal}});<br>
              &nbsp; &nbsp;  transform: rotatZ({{atomCollection[firstSelectedRotationId].rotationzfinal}});<br>
              &nbsp;  }<br>
              &nbsp;  @keyframes {{value[id].name}}_opacity_one {<br>
              &nbsp;  &nbsp;  0% {<br>
              &nbsp; &nbsp;  opacity: {{atomCollection[firstSelectedOpacityId].opacitystart / 100}};<br>
              &nbsp;  }<br>
              &nbsp;  100% {<br>
              &nbsp; &nbsp;  opacity: {{atomCollection[firstSelectedOpacityId].opacityfinal / 100 }}; <br>
              &nbsp;  }<br>
              &nbsp;  @keyframes {{value[id].name}}_scale_second {<br>
              &nbsp;  &nbsp;  0% {<br>
              &nbsp; &nbsp;  width: {{atomCollection[secondSelectedscaleId].widthstart}}px; //in pixel!<br>
              &nbsp; &nbsp;  height: {{atomCollection[secondSelectedscaleId].heightstart}}px; //in pixel!<br>
              &nbsp;  }<br>
              &nbsp;  100% {<br>
              &nbsp; &nbsp;  width: {{atomCollection[secondSelectedscaleId].widthfinal}}px; //in pixel!<br>
              &nbsp; &nbsp;  height: {{atomCollection[secondSelectedscaleId].heightfinal}}px; //in pixel!<br>
              &nbsp;  }<br>
              &nbsp;  @keyframes {{value[id].name}}_rotation_second {<br>
              &nbsp;  &nbsp;  0% {<br>
              &nbsp;  &nbsp;  transform: rotatX({{atomCollection[secondSelectedRotationId].rotationxstart}});<br>
              &nbsp;  &nbsp;  transform: rotatY({{atomCollection[secondSelectedRotationId].rotationystart}});<br>
              &nbsp;  &nbsp;  transform: rotatZ({{atomCollection[secondSelectedRotationId].rotationzstart}});<br>
              &nbsp;  }<br>
              &nbsp;  100% {<br>
              &nbsp;  &nbsp;  transform: rotatX({{atomCollection[secondSelectedRotationId].rotationxfinal}});<br>
              &nbsp;  &nbsp;  transform: rotatY({{atomCollection[secondSelectedRotationId].rotationyfinal}});<br>
              &nbsp; &nbsp;  transform: rotatZ({{atomCollection[secondSelectedRotationId].rotationzfinal}});<br>
              &nbsp;  }<br>
              &nbsp;  @keyframes {{value[id].name}}_opacity_second {<br>
              &nbsp;  &nbsp;  0% {<br>
              &nbsp; &nbsp;  opacity: {{atomCollection[secondSelectedOpacityId].opacitystart / 100}};<br>
              &nbsp;  }<br>
              &nbsp;  100% {<br>
              &nbsp; &nbsp;  opacity: {{atomCollection[secondSelectedOpacityId].opacityfinal / 100 }}; <br>
              &nbsp;  }<br>
              }
            </div>
</div>
</template>
<script>


export default {
    name: "organism",

    props: ['value', 'atomCollection', 'moleculeCollection', 'organism', 'organismid', 'globalDelay'],
    data() {
        return {
          //
          copied: false,
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
      copyThisValue(){
          return   this.value[this.id].name + this.value[this.id].orgid + "_id"
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


      firstSelectedscaleId(){
        return this.firstSelected.scaleId
      },
      firstSelectedRotationId(){
        return this.firstSelected.rotationId
      },
      firstSelectedOpacityId(){
        return this.firstSelected.opacityId
      },
      firstSelectedTranslateId(){
        return this.firstSelected.translateId
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
      secondSelectedTranslateId(){
        return this.secondSelected.translateId
      }


    },
    methods: {
        copyThis(){
          var clipboard = new Clipboard('#' + this.value[this.id].name + this.value[this.id].orgid)
          this.copied = true
          var self = this
            setTimeout(function(){
                self.copied = false;
            }, 1000);
        },
        //before animation
        beforeEnter: function(el) {
            el.style.width = this.atomCollection[this.firstSelectedscaleId].widthstart * this.value[this.id].viewPortScaleX + "px",
            el.style.height = this.atomCollection[this.firstSelectedscaleId].heightstart * this.value[this.id].viewPortScaleY + "px",
            el.style.transform = "rotateX("+ this.atomCollection[this.firstSelectedRotationId].rotationxstart +"deg)",
            el.style.transform = "rotateY("+ this.atomCollection[this.firstSelectedRotationId].rotationystart  +"deg)",
            el.style.transform = "rotateZ("+ this.atomCollection[this.firstSelectedRotationId].rotationzstart  +"deg)"
            if(this.atomCollection[this.firstSelectedTranslateId].translate || this.atomCollection[this.secondSelectedTranslateId].translate ){el.style.opacity = 0} //gegen das flackern
            Velocity(el, {
                width: this.atomCollection[this.firstSelectedscaleId].widthstart * this.value[this.id].viewPortScaleX + "px",
                height: this.atomCollection[this.firstSelectedscaleId].heightstart * this.value[this.id].viewPortScaleY + "px",
                opacity: this.atomCollection[this.firstSelectedOpacityId].opacitystart / 100,
                rotateX: this.atomCollection[this.firstSelectedRotationId].rotationxstart,
                rotateY: this.atomCollection[this.firstSelectedRotationId].rotationystart,
                rotateZ: this.atomCollection[this.firstSelectedRotationId].rotationzstart,
                translateX: +this.atomCollection[this.firstSelectedTranslateId].translateXstart    *  this.value[this.id].viewPortScaleX - 180 *  this.value[this.id].viewPortScaleX + "px",
                translateY: +this.atomCollection[this.firstSelectedTranslateId].translateYstart *  this.value[this.id].viewPortScaleY - 320 *  this.value[this.id].viewPortScaleY + "px"
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
                delay: this.globalDelay + +this.firstSelected.scaleDelay +
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
                delay: this.globalDelay + +this.firstSelected.rotationDelay +
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
                delay: this.globalDelay + +this.firstSelected.opacityDelay +
                 +this.value[this.id].firstDelay,
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
              delay: this.globalDelay + +this.firstSelected.translateDelay +
               +this.value[this.id].firstDelay,
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
                      }, 1000);
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
                      }, vm.globalDelay);
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
                      }, vm.globalDelay);

                    }
                })
              }
              if (this.secondSelectedTranslateId >= 1){
                Velocity(el, {
                  translateX: this.atomCollection[this.secondSelectedTranslateId].translateXfinal *  this.value[this.id].viewPortScaleY  - 180 *  this.value[this.id].viewPortScaleX + "px",
                  translateY: this.atomCollection[this.secondSelectedTranslateId].translateYfinal *  this.value[this.id].viewPortScaleY  - 320 *  this.value[this.id].viewPortScaleX + "px"
                }, {
                  delay: +this.secondSelected.translateDelay +
                   +this.value[this.id].secondDelay,
                  easing: this.atomCollection[this.secondSelectedTranslateId].spacing,
                  duration: this.atomCollection[this.secondSelectedTranslateId].timing,
                  queue: false,
                  complete: function() {
                    setTimeout(function(){
                      vm.nukleolus = true
                    }, vm.globalDelay);
                    }
                })
              }

          } else{
            Velocity(el, {
                backgroundColor: '#ffffff',
            }, {
                duration: 1,
                delay: this.globalDelay,
                complete: function() {

                    vm.nukleolus = true


                }
            })
          }
        }

    }

}

</script>
