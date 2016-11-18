<template>
<section class="app">
    <nav class="menu">
        <div class="menu__principles">
            <img src="./assets/principles.svg" alt="" />
        </div>
        <div class="menu__bestpractices">
            <img src="./assets/bestpractices.svg" alt="" />
        </div>
        <div class="menu__organisms">
            <img src="./assets/organisms.svg" alt="" />
        </div>
        <div class="menu__molecules">
            <img src="./assets/molecules.svg" alt="" />
        </div>
        <div class="menu__atoms">
            <img src="./assets/atoms.svg" alt="" />
        </div>
    </nav>
    <section class="universe">
        <div class="organisms__wrapper">
            <div class="anchor" id="anchor__organism">
                <h3>organisms</h3>
            </div>
            <div class="organisms">
                <div class="organism_catOne">
                    <div>
                        <!-- <h2>Organism</h2> -->
                    </div>
                    <div class="molecules__categ1" v-for="thisorganism in organism">
                        <organism :organismid="thisorganism.id" :molecule-collection="combineMoleculeCollection" :atom-collection="combineAtomCollection" v-model="organism">
                        </organism>
                    </div>
                    <button type="button" name="button" @click="addOrganismCatOne" class="organisms__addOrganism">+</button>
                </div>
            </div>
        </div>

        <div class="molecules__wrapper">
            <div class="anchor" id="anchor__molecule">
                <h3>molecules</h3>
            </div>
            <div class="molecules">
                <div class="molecule_catOne">
                    <div>
                        <!-- <h2>Molecules</h2> -->
                    </div>
                    <div class="" v-for="thismolecule in molecule">
                        <molecule :atom-collection="combineAtomCollection" v-model="molecule" :moleculeid="thismolecule.id">
                        </molecule>
                    </div>
                    <button type="button" name="button" @click="addMoleculeCatOne" class="molecules__addMolecule">+</button>
                </div>


            </div>
        </div>

        <div class="atoms__wrapper">
            <div class="anchor" id="anchor__atom">
                <h3>atoms</h3>
            </div>
            <div class="atoms">
                <div class="atoms__scale">
                    <div class="">
                        <!-- <h2>scale</h2> -->
                    </div>
                    <div v-for="thisatomscale in atomscale">
                        <atomscale v-model="atomscale" v-bind:atomscaleid="thisatomscale.id">
                        </atomscale>
                    </div>
                    <button type="button" name="button" @click="addatomscale" class="atoms__addAtom">+</button>
                </div>

                <div class="atoms__rotation">
                    <div class="">
                        <!-- <h2>Rotation</h2> -->
                    </div>
                    <div v-for="atomrotation in atomRotation">
                        <atomrotation v-model="atomRotation" v-bind:atomscaleid="atomrotation.id">
                        </atomrotation>
                    </div>
                    <button type="button" name="button" @click="addatomrotation" class="atoms__addAtom">+</button>
                </div>

                <div class="atoms__opacity">
                    <div class="">
                        <!-- <h2>Opacity</h2> -->
                    </div>
                    <div v-for="atomopacity in atomOpacity">
                        <atomopacity v-model="atomOpacity" v-bind:atomscaleid="atomopacity.id">
                        </atomopacity>
                    </div>
                    <button type="button" name="button" @click="addatomopacity" class="atoms__addAtom">+</button>
                </div>
            </div>
        </div>

        </div>

    </section>
</section>
</template>

<script>
import organism from './components/organisms/organism.vue'
import molecule from './components/molecules/molecule.vue'
import atomscale from './components/atoms/atomscale.vue'
import atomrotation from './components/atoms/atomrotation.vue'
import atomopacity from './components/atoms/atomopacity.vue'

//let atomId = 1
let currentIdscale = 0
let currentIdRotation = 0
let currentIdOpacity = 0

export default {
    name: 'universe',
    components: {
        atomrotation,
        atomscale,
        atomopacity,
        molecule,
        organism,
    },
    data() {
        return {
            atomId: 3, //start bei 2 weil atomscale und atomRotation und atomOpacity und atomNull für den prototypen schon gesetzt sind
            viewportX: 360,
            viewportY: 640,
            atomViewportX: 168.75,
            atomViewportY: 300,
            moleculeViewportX: 196.88,
            moleculeViewportY: 350,
            organismViewportX: 281.25,
            organismViewportY: 500,


            atomCollection: [],
            atomscale: [{
                id: 0,
                name: "Bromine-Scale",
                timing: "250",
                spacing: "easeOutSine",
                widthstart: "50",
                widthfinal: "200",
                heightstart: "50",
                heightfinal: "200",
                atomid: 1,
                viewPortScaleX: 0.46875,
                viewPortScaleY: 0.46875
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
                atomid: 2,
                viewPortScaleX: 0.46875,
                viewPortScaleY: 0.46875
            }],
            atomOpacity: [{
                id: 0,
                name: "Indium-Opacity",
                timing: "250",
                spacing: "easeOutSine",
                opacitystart: "0",
                opacityfinal: "100",
                atomid: 3,
                viewPortScaleX: 0.46875,
                viewPortScaleY: 0.46875
            }],
            atomNull: [{
                name: "-",
                atomid: 0,
                opacitystart: 100,
                opacityfinal: 100,
                rotationzfinal: "0",
                widthstart: "50",
                heightstart: "50",
                widthfinal: "50",
                heightfinal: "50",
                atomid: 0,
                id: 0,
                viewPortScaleX: 0.46875,
                viewPortScaleY: 0.46875
            }],

            //
            moleculeId: 0,
            moleculeid: 1,
            moleculeCollection: [],
            molecule: [{
                name: "Maltol-Molecule",
                scaleId: 0,
                scaleDelay: 0,
                rotationId: 0,
                rotationDelay: 0,
                opacityId: 0,
                opacityDelay: 0,
                id: 0,
                molid: 1,
                viewPortScaleX: 0.546875,
                viewPortScaleY: 0.546875
            }],
            moleculeNull: [{
                name: "-",
                scaleId: 0,
                scaleDelay: 0,
                rotationId: 0,
                rotationDelay: 0,
                opacityId: 0,
                opacityDelay: 0,
                id: 0,
                molid: 0,
                viewPortScaleX: 0.546875,
                viewPortScaleY: 0.546875
            }],

            //
            organismId: 0,
            orgid: 1,
            organismCollection: [],
            organism: [{
                name: "Sarkodina-Organism",
                id: 0,
                firstMoleculeId: 0,
                firstDelay: 0,
                secondMoleculeId: 0,
                secondDelay: 0,
                thirdMoleculeId: 0,
                thridDelay: 0,
                orgid: 1,
                viewPortScaleX: 0.78125,
                viewPortScaleY: 0.78125
            }],
            organismNull: [{
                name: "-",
                id: 0,
                firstMoleculeId: 0,
                firstDelay: 0,
                secondMoleculeId: 0,
                secondDelay: 0,
                thirdMoleculeId: 0,
                thridDelay: 0,
                orgid: 0,
                viewPortScaleX: 0.78125,
                viewPortScaleY: 0.78125
            }],

            //
            randomElements: ['Hydrogen', 'Helium', 'Lithium', 'Beryllium', 'Boron', 'Carbon', 'Nitrogen', 'Oxygen', 'Fluorine', 'Neon', 'Sodium', 'Magnesium'],
            randomMolecules: ['Acetone', 'Chromium ', 'Fluorite', 'Hexane', 'Jadeite', 'Niter', 'Picene', 'Tamoxifen', 'Topaz', 'Water', 'Zircon', 'Vanillin'],
            randomOrganisms: ['Cupulata', 'Mucorina', 'Astoma', 'Sporoza', 'Floridea', 'Diatomea', 'Bangialea', 'Fuciodea', 'Fungi', 'Exosporea', 'Heliozoa', 'Nuda'],

        }
    },
    computed: {

        combineAtomCollection() {
            return this.atomCollection.concat(this.atomNull, this.atomscale, this.atomRotation, this.atomOpacity)
        },
        combineMoleculeCollection() {
            return this.moleculeCollection.concat(this.moleculeNull, this.molecule)
        },
        combineOrganismCollection() {
            return this.moleculeCollection.concat(this.organismNull, this.organism)
        },
        atomViewPortScaleX() {
            return this.atomViewportX / this.viewportX
        },
        atomViewPortScaleY() {
            return this.atomViewportY / this.viewportY
        },
        moleculeViewPortScaleX() {
            return this.moleculeViewportX / this.viewportX
        },
        moleculeViewPortScaleY() {
            return this.moleculeViewportY / this.viewportY
        },
        organismViewPortScaleX() {
            return this.organismViewportX / this.viewportX
        },
        organismViewPortScaleY() {
            return this.organismViewportY / this.viewportY
        }

    },
    methods: {
        addOrganismCatOne() {
            this.organismId++,
                this.orgid++,
                this.organism.push({
                    name: this.randomMolecules[Math.floor((Math.random() * 11) + 1)] + "-Organism",
                    id: this.organismId,
                    firstMoleculeId: 0,
                    firstDelay: 0,
                    secondMoleculeId: 0,
                    secondDelay: 0,
                    thirdMoleculeId: 0,
                    thridDelay: 0,
                    orgid: this.orgid,
                    viewPortScaleX: this.organismViewPortScaleX,
                    viewPortScaleY: this.organismViewPortScaleY
                })
        },
        addMoleculeCatOne() {
            this.moleculeId++,
                this.moleculeid++,
                this.molecule.push({
                    name: this.randomMolecules[Math.floor((Math.random() * 11) + 1)] + "-Molecule",
                    scaleId: 0,
                    scaleDelay: 0,
                    rotationId: 0,
                    rotationDelay: 0,
                    opacityId: 0,
                    opacityDelay: 0,
                    id: this.moleculeId,
                    molid: this.moleculeid,
                    viewPortScaleX: this.moleculeViewPortScaleX,
                    viewPortScaleY: this.moleculeViewPortScaleY
                })
        },
        // properties der atome
        addatomscale() {
            this.atomId++,
                currentIdscale++,
                this.atomscale.push({
                    id: currentIdscale,
                    name: this.randomElements[Math.floor((Math.random() * 11) + 1)] + "-Scale",
                    timing: "250",
                    spacing: "easeOutSine",
                    widthstart: "50",
                    widthfinal: "200",
                    heightstart: "50",
                    heightfinal: "200",
                    atomid: this.atomId,
                    viewPortScaleX: this.atomViewPortScaleX,
                    viewPortScaleY: this.atomViewPortScaleY
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
                    atomid: this.atomId,
                    viewPortScaleX: this.atomViewPortScaleX,
                    viewPortScaleY: this.atomViewPortScaleY
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
                    atomid: this.atomId,
                    viewPortScaleX: this.atomViewPortScaleX,
                    viewPortScaleY: this.atomViewPortScaleY
                })
        }
    },

}
</script>

<style lang="sass">@import './scss/main.scss'</style>
