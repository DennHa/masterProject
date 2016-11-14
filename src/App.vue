<template>
<section class="universe">
    <div class="molecules__wrapper">
      <div class="organisems">
          <div>
              <div>
                  <h2>Organisem</h2>
              </div>
              <div class="molecules__categ1" v-for="thisorganisem in organisem">
                  <molecule :atom-collection="combineMoleculeCollection" >
                  </molecule>
              </div>
          </div>
      </div>
        <div class="molecules">
            <div>
                <div>
                    <h2>Molecules</h2>
                </div>
                <div class="molecules__categ1" v-for="thismolecule in molecule">
                    <molecule :atom-collection="combineAtomCollection" v-model="molecule" :moleculeid="thismolecule.id">
                    </molecule>
                </div>
                <button type="button" name="button" @click="addmoleculeCateg1" class="molecules__addMolecule">+</button>
            </div>
        </div>
    </div>

    <div class="atoms__wrapper">
        <div class="atoms">
            <div class="atoms__size">
                <div class="">
                    <h2>Size</h2>
                </div>
                <div v-for="atomsize in atomSize">
                    <atomsize v-model="atomSize" v-bind:atomsizeid="atomsize.id">
                    </atomsize>
                </div>
                <button type="button" name="button" @click="addatomsize" class="atoms__addAtom">+</button>
            </div>

            <div class="atoms__rotation">
                <div class="">
                    <h2>Rotation</h2>
                </div>
                <div v-for="atomrotation in atomRotation">
                    <atomrotation v-model="atomRotation" v-bind:atomsizeid="atomrotation.id">
                    </atomrotation>
                </div>
                <button type="button" name="button" @click="addatomrotation" class="atoms__addAtom">+</button>
            </div>

            <div class="atoms__opacity">
                <div class="">
                    <h2>Opacity</h2>
                </div>
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
    data() {
        return {
            atomId: 3, //start bei 2 weil atomSize und atomRotation und atomOpacity und atomNull für den prototypen schon gesetzt sind

            moleculeId: 0,

            atomCollection: [],
            atomSize: [{
                id: 0,
                name: "Bromine-Size",
                timing: "250",
                spacing: "easeOutSine",
                widthstart: "50",
                widthfinal: "100",
                heightstart: "50",
                heightfinal: "100",
                atomid: 1
            }],
            atomRotation: [{
                id: 0,
                name: "Yttrium-Rotation",
                timing: "250",
                spacing: "easeOutSine",
                rotationxstart: "0",
                rotationxfinal: "0",
                rotationystart: "0",
                rotationyfinal: "0",
                rotationzstart: "0",
                rotationzfinal: "45",
                atomid: 2
            }],
            atomOpacity: [{
                id: 0,
                name: "Indium-Opacity",
                timing: "250",
                spacing: "easeOutSine",
                opacitystart: "0",
                opacityfinal: "100",
                atomid: 3
            }],
            atomNull: [{
                name: "-",
                atomid: 0,
                opacitystart: 100,
                opacityfinal: 100,
                rotationzfinal: "0",
                widthstart: "20",
                heightstart: "20",
                widthfinal: "20",
                heightfinal: "20",
                atomid: 0,
                id: 0
            }],

            //
            moleculeCollection: [],
            molecule: [{
                name: "Samarium-Molecule",
                sizeId: 0,
                sizeDelay: 0,
                rotationId: 0,
                rotationDelay: 0,
                opacityId: 0,
                opacityDelay: 0,
                id: 0
            }],
            moleculeNull: [{
                name: "-",
                sizeId: 0,
                sizeDelay: 0,
                rotationId: 0,
                rotationDelay: 0,
                opacityId: 0,
                opacityDelay: 0,
                id: 0
            }],

            organisem: [{
              name: "hey"
            }],

            //
            randomElements: ['Hydrogen', 'Helium', 'Lithium', 'Beryllium', 'Boron', 'Carbon', 'Nitrogen', 'Oxygen', 'Fluorine', 'Neon', 'Sodium', 'Magnesium'],

        }
    },
    computed: {

        combineAtomCollection() {
            return this.atomCollection.concat(this.atomNull, this.atomSize, this.atomRotation, this.atomOpacity)

        },
        combineMoleculeCollection() {
            return this.moleculeCollection.concat(this.moleculeNull, this.molecule)
        },

    },
    methods: {
        addmoleculeCateg1() {
            this.moleculeId++,
                this.molecule.push({
                    name: this.randomElements[Math.floor((Math.random() * 11) + 1)] + "-Molecule",
                    sizeId: 0,
                    sizeDelay: 0,
                    rotationId: 0,
                    rotationDelay: 0,
                    opacityId: 0,
                    opacityDelay: 0,
                    id: this.moleculeId
                })
        },
        // properties der atome
        addatomsize() {
            this.atomId++,
                currentIdSize++,
                this.atomSize.push({
                    id: currentIdSize,
                    name: this.randomElements[Math.floor((Math.random() * 11) + 1)] + "-Size",
                    timing: "250",
                    spacing: "easeOutSine",
                    widthstart: "50",
                    widthfinal: "100",
                    heightstart: "50",
                    heightfinal: "100",
                    atomid: this.atomId
                })
        },
        addatomrotation() {
            this.atomId++,
                currentIdRotation++,
                this.atomRotation.push({
                    id: currentIdRotation,
                    name: this.randomElements[Math.floor((Math.random() * 11) + 1)] + "-Rotation",
                    timing: "250",
                    spacing: "easeOutSine",
                    rotationxstart: "0",
                    rotationxfinal: "0",
                    rotationystart: "0",
                    rotationyfinal: "0",
                    rotationzstart: "0",
                    rotationzfinal: "45",
                    atomid: this.atomId
                })
        },
        addatomopacity() {
            this.atomId++,
                currentIdOpacity++,
                this.atomOpacity.push({
                    id: currentIdOpacity,
                    name: this.randomElements[Math.floor((Math.random() * 11) + 1)] + "-Opacity",
                    timing: "250",
                    spacing: "easeOutSine",
                    opacitystart: "0",
                    opacityfinal: "100",
                    atomid: this.atomId
                })
        }
    },

}
</script>

<style lang="sass">@import './scss/main.scss'</style>
