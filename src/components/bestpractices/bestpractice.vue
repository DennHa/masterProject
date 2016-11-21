<template name="bestpractice">
<div class="bestpractice__bond">
    <div class="bestpractice__viewerExample" v-if="!showLive">
        <h3>Drop File Here</h3>
        <img src="../../assets/ps4.gif" alt="" v-if="value[id].id == 0" />
    </div>
    <div class="bestpractice__viewer" v-if="showLive">

        <div class="hitarea" v-on:click="touchIt++" v-bind:style="{width: hitareaWidth + 'px', height: hitareaHeight + 'px', top: hitareaYpos + 'px', left: hitareaXpos + 'px', opacity: hitareaOpacity }"  v-if="chooseInteraction == 'touch'"></div>

        <nukleolus :molecule-collection="moleculeCollection" :atom-collection="atomCollection" :organism-collection="organismCollection" element="0" v-model="value" :this-delay="value[id].firstElementDelay" :global-delay="globalDelay" :interaction="interaction" :interacted="touchIt">
        </nukleolus>
        <nukleolus :molecule-collection="moleculeCollection" :atom-collection="atomCollection" :organism-collection="organismCollection" element="1" v-model="value" v-if="value[id].secondElement >= 1" :this-delay="value[id].secondElementDelay" :global-delay="globalDelay" :interaction="interaction" :interacted="touchIt" >
        </nukleolus>
        <nukleolus :molecule-collection="moleculeCollection" :atom-collection="atomCollection" :organism-collection="organismCollection" element="2" v-model="value" v-if="value[id].thirdElement >= 1" :this-delay="value[id].thirdElementDelay" :global-delay="globalDelay" :interaction="interaction" :interacted="touchIt" >
        </nukleolus>

    </div>
    <div class="bestpractice__properties">
        <h3>bestpractice</h3>
        <form class="" action="index.html" method="post">
            <input name="name" class="atom__name" v-model="value[id].name">
        </form>
        <div>

            <select class="bestpractice__kind" v-model="chooseInteraction" >
             <option>
               autoplay
             </option>
             <option>
               touch
             </option>
          </select>
          <span class="connectedIt">-></span>
        <select class="bestpractice__kind" v-model="value[id].firstElement">
           <option v-for="element in organismCollection" :value="element.orgid">
             {{ element.name }}
           </option>
        </select>
        <span class="connectedIt" v-if="value[id].firstElement >= 1">&</span>
            <select class="bestpractice__kind" v-model="value[id].secondElement" v-if="value[id].firstElement >= 1">
           <option  v-for="element in organismCollection" :value="element.orgid">
             {{ element.name }}
           </option>
        </select>
            <span class="connectedIt" v-if="value[id].secondElement >= 1">&</span>
            <select class="bestpractice__kind" v-model="value[id].thirdElement" v-if="value[id].secondElement >= 1">

           <option  v-for="element in organismCollection" :value="element.orgid">
             {{ element.name }}
           </option>
        </select>
        </div>


        <div class="bestpractice__timing">
            <div class="bestpractice__scaleDelay" v-if="value[id].firstElement >= 1">
                <h3>first delay {{value[id].firstElementDelay}}</h3>
                <input type="range" v-model="value[id].firstElementDelay" min="0" max="1000" step="10" defaultValue="0">
            </div>
            <div class="bestpractice__rotationDelay" v-if="value[id].secondElement >= 1">
                <h3>second delay {{value[id].secondElementDelay}}</h3>
                <input type="range" v-model="value[id].secondElementDelay" min="0" max="1000" step="10" defaultValue="0">
            </div>
            <div class="bestpractice__rotationDelay" v-if="value[id].thirdElement >= 1">
                <h3>third delay {{value[id].secondElementDelay}}</h3>
                <input type="range" v-model="value[id].secondElementDelay" min="0" max="1000" step="10" defaultValue="0">
            </div>
        </div>
        <!-- <div class="">

          <input type="radio" id="auto" value="auto" v-model="interaction">
          <label for="one">auto play</label>

        </div>

        <div class="">
          <input type="radio" id="touch" value="touch" v-model="interaction">
          <label for="two">touch</label>
        </div> -->
        <div class="hitareaProperties" v-if="chooseInteraction == 'touch' && showLive">
          <span class="warning" >Inputs aren't supported yte</span>
          <form>
            <input type="number" name="name" value="" v-model="hitareaWidth"><label for="two"> hitarea width</label><br>
            <input type="number" name="name" value="" v-model="hitareaHeight"><label for="two"> hitarea height</label><br>
            <input type="number" name="name" value="" v-model="hitareaXpos"><label for="two"> posX</label><br>
            <input type="number" name="name" value="" v-model="hitareaYpos"><label for="two"> posY</label><br>
            <input type="checkbox" name="name" value="" v-model="hideHitarea"><label for="two"> hide hitarea</label>
          </form>
        </div>
    </div>
    <div class="subMenuSwap">
        <div v-on:click="showLive = !showLive"></div>

    </div>
</div>
</template>
<script>
//import Dropzone from '../../../lib/Dropzone'
//import Dropzone from './Dropzone.vue'
//import Dropzone from 'dropzone'
import nukleolus from './nukleolus_bp.vue'

export default {

    name: "bestpractice",
    components: {
        nukleolus
    },

    props: ['value', 'atomCollection', 'moleculeCollection', 'bestpractice', 'bestpracticeid', 'organismCollection', 'globalDelay'],
    data() {
        return {
            interaction: "auto",
            copied: false,
            nukleolus: true,
            selected: "",
            showLive: false,
            hitareaWidth: 50,
            hitareaHeight: 50,
            hitareaXpos: 0,
            hitareaYpos: 0,
            hideHitarea: false,
            interacted: false,
            touchIt: 1,
            chooseInteraction: "autoplay"

        }
    },
    mounted(){
      touchIt: 1
    },
    computed: {
        id() {
            return this.bestpracticeid
        },
        hitareaOpacity() {
            if(this.hideHitarea == false){
              return 0.15
            }
            return 0
        }

    },
    methods: {

    }

}
</script>
