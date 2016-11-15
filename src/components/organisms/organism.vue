<template name="organism">
<div class="molecule__bond">

    <div class="molecule__viewer">
        <!-- <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
            <div class="molecule__nukleolus" v-if="nukleolus"></div>
        </transition> -->
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


    },

    // methods: {
    //
    //     //before animation
    //     beforeEnter: function(el) {
    //         el.style.width = this.firstSelected.widthstart + "%",
    //         el.style.height = this.firstSelected.heightstart + "%",
    //         el.style.transform = "rotateX("+ this.secondSelected.rotationxstart +"deg)",
    //         el.style.transform = "rotateY("+ this.secondSelected.rotationystart  +"deg)",
    //         el.style.transform = "rotateZ("+ this.secondSelected.rotationzstart  +"deg)",
    //         el.style.opacity = this.thirdSelected.opacitystart / 100
    //
    //     },
    //
    //     //animation enter
    //     enter: function(el, done) {
    //         var vm = this
    //         Velocity(el, {
    //           width: this.firstSelected.widthfinal + "%",
    //           height: this.firstSelected.heightfinal + "%"
    //
    //         }, {
    //             delay: 2000 + +this.value[this.id].sizeDelay,
    //             easing: this.firstSelected.spacing,
    //             duration: this.firstSelected.timing,
    //             complete: function() {
    //                done()
    //                if (!vm.stop) vm.nukleolus = false
    //             }
    //         })
    //         Velocity(el, {
    //
    //           rotateX: this.secondSelected.rotationxfinal + "deg",
    //           rotateY: this.secondSelected.rotationyfinal + "deg",
    //           rotateZ: this.secondSelected.rotationzfinal + "deg"
    //         }, {
    //             delay: 2000 + +this.value[this.id].rotationDelay,
    //             easing: this.secondSelected.spacing,
    //             duration: this.secondSelected.timing,
    //             queue: false,
    //             complete: function() {
    //                done()
    //                if (!vm.stop) vm.nukleolus = false
    //             }
    //         })
    //         Velocity(el, {
    //           opacity: this.thirdSelected.opacityfinal / 100,
    //         }, {
    //             delay: 2000 + +this.value[this.id].opacityDelay,
    //             easing: this.thirdSelected.spacing,
    //             duration: this.thirdSelected.timing,
    //             queue: false,
    //             complete: function() {
    //                done()
    //                if (!vm.stop) vm.nukleolus = false
    //             }
    //         })
    //
    //     },
    //
    //     //animation leave - just for restart
    //     leave: function(el, done) {
    //         var vm = this
    //         Velocity(el, {
    //             backgroundColor: '#ffffff',
    //         }, {
    //             duration: 1,
    //             delay: "2000",
    //             complete: function() {
    //                 done()
    //                 vm.nukleolus = true
    //             }
    //         })
    //     }
    // },

}

</script>
