<template name="principle">
    <div class="principle__bond">
        <div class="principle__properties">
          <div class="principle__text" style="z-index: 200" v-html="compiledMarkdown" v-if="!editText" v-on:click="editText = true"></div>

          <textarea style="z-index: 200" name="name" :value="input" @input="update" v-if="editText"></textarea>
          <div class="subMenuEditText">
              <div v-on:click="editText = !editText"></div>
          </div>
        </div>
        <div class="showExample" v-if="editText">
          <label for="example">show Example</label>
          <input type="checkbox" id="example" value="example" style="z-index: 201" v-model="showIt">
        </div>
        <showcase :atomcollection="atomCollection" :showcase="showcase"  :thismoleculeid="principleid" :global-delay="globalDelay" v-if="editText || showIt == true"></showcase>

    </div>
</template>
<script>
import showcase from './showcase.vue'
var _ = require('lodash');
var marked = require('marked');
export default {

    name: "principle",
    components: {
        showcase
    },
    props: ['value', 'principleid', 'molecule','moleculeid', 'globalDelay', "atomCollection"],
    data() {
        return {
          showIt: false,
          editText: false
        }
    },
    mounted(){

    },
    computed: {
      showcase(){
        return this.molecule
      },
      input() {
        if (this.principleid == 0){
          return '# Temperature <!-- Wirte Markedown --> <h2>Documenting Dynamic and Interactive UI Elements</h2><p> Prototype made by 🖖 <a href="https://www.dennishatwieger.de">Dennis Hatwieger</a> 🖖</p> '
        }
        else {
          return '## Principle #' + this.principleid
        }

      },
      compiledMarkdown: function () {
        return marked(this.input, {gfm: true, breaks: true })
      }
    },
    methods: {
      update: _.debounce(function (e) {
        this.input = e.target.value
      }, 300),


    }


}
</script>
