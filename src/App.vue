<template>
<section class="universe">
  <div class="molecules">
    <molecule :atom-collection="combineAtomCollection">
    </molecule>
  </div>

  <div class="atoms__wrapper">
  <div class="atoms">
    <div class="atoms__size">
      <h2>Size</h2>
      <div v-for="atomsize in atomSize" >
        <atomsize v-model="atomSize" v-bind:atomsizeid="atomsize.id">
        </atomsize>
      </div>
      <button type="button" name="button" @click="addatomsize" class="atoms__addAtom">+</button>
    </div>

    <div class="atoms__rotation">
      <h2>Rotation</h2>
      <div v-for="atomrotation in atomRotation">
        <atomrotation v-model="atomRotation" v-bind:atomsizeid="atomrotation.id">
        </atomrotation>
      </div>
      <button type="button" name="button" @click="addatomrotation" class="atoms__addAtom">+</button>
    </div>

    <div class="atoms__opacity">
      <h2>Opacity</h2>
      <div v-for="atomopacity in atomOpacity">
        <atomopacity v-model="atomOpacity" v-bind:atomsizeid="atomopacity.id">
        </atomopacity>
      </div>
      <button type="button" name="button" @click="addatomopacity" class="atoms__addAtom">+</button>
    </div>
  </div>
  </div>

</div>

</section>
</template>

<script>
import molecule from './components/molecules/molecule.vue'
import atomsize from './components/atoms/atomsize.vue'
import atomrotation from './components/atoms/atomrotation.vue'
import atomopacity from './components/atoms/atomopacity.vue'

//let atomId = 1
let currentIdSize = 0
let currentIdRotation = 0
let currentIdOpacity = 0

export default {
  name: 'universe',
  components: {
    atomrotation,
    atomsize,
    atomopacity,
    molecule
  },
  data () {
    return {
      atomId: 3, //start bei 2 weil atomSize und atomRotation und atomOpacity und atomNull für den prototypen schon gesetzt sind

      atomCollection:[],
      atomSize:[
        {id: 0, name: "Size", timing: "250", spacing: "easeOutSine", widthstart: "50", widthfinal:"100", heightstart: "50", heightfinal: "100", atomid: 1}
      ],
      atomRotation:[
        {id: 0, name: "Rotation", timing: "250", spacing: "easeOutSine", rotationxstart: "0", rotationxfinal:"0", rotationystart: "0", rotationyfinal: "0", rotationzstart: "0", rotationzfinal: "45", atomid: 2}
      ],
      atomOpacity:[
        {id: 0, name: "Opacity", timing: "250", spacing: "easeOutSine", opacitystart: "0", opacityfinal:"100", atomid: 3}
      ],
      atomNull:[{name: "-", atomid: 0, opacitystart: 100, opacityfinal: 100, rotationzfinal: "0",widthstart:"20", heightstart:"20", widthfinal: "20", heightfinal:"20", atomid: 0, id: 0}]

    }
  },
  computed:{
    combineAtomCollection(){
      return this.atomCollection.concat(this.atomNull, this.atomSize, this.atomRotation, this.atomOpacity)

    }
  },
  methods:{

    // properties der atome
    addatomsize(){
      this.atomId ++,
      currentIdSize ++,
      this.atomSize.push({id: currentIdSize, name: "Size " + currentIdSize, timing: "250", spacing: "easeOutSine", widthstart: "50", widthfinal:"100", heightstart: "50", heightfinal: "100", atomid: this.atomId})
    },
    addatomrotation(){
      this.atomId ++,
      currentIdRotation ++,
      this.atomRotation.push({id: currentIdRotation, name: "Rotation " + currentIdRotation, timing: "250", spacing: "easeOutSine", rotationxstart: "0", rotationxfinal:"0", rotationystart: "0", rotationyfinal: "0", rotationzstart: "0", rotationzfinal: "45", atomid: this.atomId})
    },
    addatomopacity(){
      this.atomId ++,
      currentIdOpacity ++,
      this.atomOpacity.push({id: currentIdOpacity, name: "Opacity " + currentIdOpacity, timing: "250", spacing: "easeOutSine", opacitystart: "0", opacityfinal:"100", atomid: this.atomId})
    }
  },

}

</script>

<style lang="sass">
  @import './scss/main.scss'
</style>
