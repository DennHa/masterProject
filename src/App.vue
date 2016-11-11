<template>
<section class="universe">
  <div class="molecules">
    <molecule :atom-collection="combineAtomCollection">
    </molecule>
  </div>

  <div class="atoms">
    <div class="atoms__size">
      <h2>Size</h2>
      <div v-for="atomsize in atomSize" >
        <atomsize v-model="atomSize" v-bind:atomsizeid="atomsize.id">
        </atomsize>
      </div>
      <button type="button" name="button" @click="addatomsize">Add Size</button>
    </div>

    <div class="atoms__rotation">
      <h2>Rotation</h2>
      <div v-for="atomrotation in atomRotation">
        <atomrotation v-model="atomRotation" v-bind:atomsizeid="atomrotation.id">
        </atomrotation>
      </div>
      <button type="button" name="button" @click="addatomrotation">Add Size</button>
    </div>
  </div>

</section>
</template>

<script>
import molecule from './components/molecules/molecule.vue'
import atomsize from './components/atoms/atomsize.vue'
import atomrotation from './components/atoms/atomrotation.vue'

//let atomId = 1
let currentIdSize = 0
let currentIdRotation = 0

export default {
  name: 'universe',
  components: {
    atomrotation,
    atomsize,
    molecule
  },
  data () {
    return {
      atomId: 1, //start bei 1 weil atomSize und atomRotation für den prototypen schon gesetzt sind

      atomCollection:[],
      atomSize:[
        {id: 0, name: "Size", timing: "250", spacing: "easeOutSine", widthstart: "50", widthfinal:"100", heightstart: "50", heightfinal: "100", atomid: 0}
      ],
      atomRotation:[
        {id: 0, name: "Rotation", timing: "250", spacing: "easeOutSine", rotationxstart: "0", rotationxfinal:"0", rotationystart: "0", rotationyfinal: "0", rotationzstart: "0", rotationzfinal: "45", atomid: 1}
      ]
    }
  },
  computed:{
    combineAtomCollection(){
      return this.atomCollection.concat(this.atomSize, this.atomRotation)

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
    }
  },

}

</script>

<style lang="sass">
  @import './scss/main.scss'
</style>
