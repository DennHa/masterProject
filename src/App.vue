<template>
<section class="universe">
  <div class="atoms" >
    <span v-for="numberAtom in numberAtoms">
      <button type="button" @click="woo" name="button"></button>
      <atom></atom><!--  v-on:clickRemove="removeThisAtom" -->
    </span>
  </div>
  <button v-on:click="add">Add</button>
</section>
</template>

<script>
import atom from './components/atoms/atom.vue'
var foo = "hey"

let currentAtomId = 1

export default {
  name: 'universe',
  components: {
    atom
  },
  data () {
    return {
      numberAtoms: [{id: "1" }],
      close: "",
      thisProb: null
    }
  },
  mounted(){
  },
  methods: {
    removeThisAtom(){
      this.close = true
    },
    add: function() {
      console.log(this)
      currentAtomId ++
      return this.numberAtoms.push({ id: currentAtomId })
    },
    woo(){
      alert(foo)
    }
  },
  computed:{
    removeThisAtom: function(){
      close = false
    }
  }

}

</script>

<style lang="sass">
@import './scss/main.scss';
</style>
