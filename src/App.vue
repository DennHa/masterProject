<template>
<section class="app">
    <span class="menu__wrapper">
      <nav class="menu" data-gumshoe >
              <a class="menu__principles" data-scroll href="#anchor__principle">
                  <img src="./assets/principles.svg" alt=""  />
              </a>
              <a class="menu__bestpractices" data-scroll href="#anchor__bestpractice">
                  <img src="./assets/bestpractices.svg" alt="" />
              </a>
              <a class="menu__organisms" data-scroll href="#anchor__organism">
                  <img src="./assets/organisms.svg" alt="" />
              </a>
              <a class="menu__molecules" data-scroll href="#anchor__molecule">
                  <img src="./assets/molecules.svg" alt="" />
              </a>
              <a class="menu__atoms" data-scroll href="#anchor__atom">
                  <img src="./assets/atoms.svg" alt="" />
              </a>
      </nav>
    </span>
    <section class="universe">
      <div class="principles__wrapper" id="anchor__principle">
          <div class="anchor">
              <h3>principle</h3>
          </div>
          <div class="principles">
              <div class="principle_catOne">
                  <div>
                      <!-- <h2>Organism</h2> -->
                  </div>
                  <div class="" v-for="thisprinciple in principle">
                      <principle v-model="principle" :principleid="thisprinciple.id" :atom-collection="combineAtomCollection" v-bind:molecule="molecule"   :global-delay="globalDelay">
                      </principle>
                  </div>
                  <button type="button" name="button" @click="addPrincipleCatOne" class="principles__addPrinciple">+</button>
              </div>
          </div>
      </div>
      <div class="bestpractices__wrapper" id="anchor__bestpractice">
          <div class="anchor">
              <h3>bestpractice</h3>
          </div>
          <div class="bestpractices">
              <div class="bestpractice_catOne">
                  <div>
                      <!-- <h2>Organism</h2> -->
                  </div>
                  <div class="" v-for="thisbestpractice in bestpractice">
                      <bestpractice :bestpracticeid="thisbestpractice.id" :molecule-collection="combineMoleculeCollection" :atom-collection="combineAtomCollection" :organism-collection="combineOrganismCollection" v-model="bestpractice" :global-delay="globalDelay">
                      </bestpractice>
                  </div>
                  <button type="button" name="button" @click="addBestPracticeCatOne" class="organisms__addOrganism">+</button>
              </div>
          </div>
      </div>
        <div class="organisms__wrapper" id="anchor__organism">
            <div class="anchor">
                <h3>organisms</h3>
            </div>
            <div class="organisms">
                <div class="organism_catOne">
                    <div>
                        <!-- <h2>Organism</h2> -->
                    </div>
                    <div class="molecules__categ1" v-for="thisorganism in organism">
                        <organism :organismid="thisorganism.id" :molecule-collection="combineMoleculeCollection" :atom-collection="combineAtomCollection" v-model="organism" :global-delay="globalDelay">
                        </organism>
                    </div>
                    <button type="button" name="button" @click="addOrganismCatOne" class="organisms__addOrganism">+</button>
                </div>
            </div>
        </div>

        <div class="molecules__wrapper" id="anchor__molecule">
            <div class="anchor" >
                <h3>molecules</h3>
            </div>
            <div class="molecules">
                <div class="molecule_catOne">
                    <div>
                        <!-- <h2>Molecules</h2> -->
                    </div>
                    <div class="" v-for="thismolecule in molecule">
                        <molecule :atom-collection="combineAtomCollection" v-model="molecule" :moleculeid="thismolecule.id" :global-delay="globalDelay">
                        </molecule>
                    </div>
                    <button type="button" name="button" @click="addMoleculeCatOne" class="molecules__addMolecule">+</button>
                </div>


            </div>
        </div>

        <div class="atoms__wrapper" id="anchor__atom">
            <div class="anchor" >
                <h3>atoms</h3>
            </div>
            <div class="atoms">
                <div class="atoms__scale">
                    <div class="">
                        <!-- <h2>scale</h2> -->
                    </div>
                    <div v-for="thisatomscale in atomscale">
                        <atomscale v-model="atomscale" v-bind:atomscaleid="thisatomscale.id" :global-delay="globalDelay">
                        </atomscale>
                    </div>
                    <button type="button" name="button" @click="addatomscale" class="atoms__addAtom">+</button>
                </div>
                <div class="atoms__translate">
                    <div class="">
                        <!-- <h2>translate</h2> -->
                    </div>
                    <div v-for="atomtranslate in atomTranslate">
                        <atomtranslate v-model="atomTranslate" v-bind:atomtranslateid="atomtranslate.id" :global-delay="globalDelay">
                        </atomtranslate>
                    </div>
                    <button type="button" name="button" @click="addatomtranslate" class="atoms__addAtom">+</button>
                </div>

                <div class="atoms__rotation">
                    <div class="">
                        <!-- <h2>Rotation</h2> -->
                    </div>
                    <div v-for="atomrotation in atomRotation">
                        <atomrotation v-model="atomRotation" :global-delay="globalDelay" v-bind:atomscaleid="atomrotation.id">
                        </atomrotation>
                    </div>
                    <button type="button" name="button" @click="addatomrotation" class="atoms__addAtom">+</button>
                </div>

                <div class="atoms__opacity">
                    <div class="">
                        <!-- <h2>Opacity</h2> -->
                    </div>
                    <div v-for="atomopacity in atomOpacity">
                        <atomopacity v-model="atomOpacity" :global-delay="globalDelay" v-bind:atomscaleid="atomopacity.id">
                        </atomopacity>
                    </div>
                    <button type="button" name="button" @click="addatomopacity" class="atoms__addAtom">+</button>
                </div>
            </div>
        </div>
    </section>
    <section class="global">
      <form class="" action="" method="post">
      <span>globalDelay(ms)</span>  <input  name="name" value="" v-model="globalDelay" type="number">
      </form>
    </section>
</section>
</template>

<script>
import organism from './components/organisms/organism.vue'
import bestpractice from './components/bestpractices/bestpractice.vue'
import molecule from './components/molecules/molecule.vue'
import atomscale from './components/atoms/atomscale.vue'
import atomrotation from './components/atoms/atomrotation.vue'
import atomopacity from './components/atoms/atomopacity.vue'
import atomtranslate from './components/atoms/atomtranslate.vue'
import principle from './components/principles/principle.vue'

//let atomId = 1
let currentIdscale = 0
let currentIdRotation = 0
let currentIdOpacity = 0
let currentIdTranslate = 0


export default {
    name: 'universe',
    components: {
        atomrotation,
        atomtranslate,
        atomscale,
        atomopacity,
        molecule,
        organism,
        bestpractice,
        principle
    },
    data() {
        return {
          globalDelay: 2000,
            atomId: 4, //start bei 2 weil atomscale und atomtranslate und atomRotation und atomOpacity und atomNull für den prototypen schon gesetzt sind
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
                name: "BromineScale",
                timing: 250,
                spacing: "easeOutSine",
                widthstart: 50,
                widthfinal: 200,
                heightstart: 50,
                heightfinal: 200,
                atomid: 1,
                viewPortScaleX: 0.46875,
                viewPortScaleY: 0.46875
            }],
            atomTranslate: [{
                id: 0,
                name: "CobaltTranslate",
                timing: 250,
                spacing: "easeOutSine",
                translate: true,
                translateXstart: 0,
                translateXfinal: 360,
                translateYstart: 0,
                translateYfinal: 640,
                atomid: 4,
                viewPortScaleX: 0.46875,
                viewPortScaleY: 0.46875
            }],
            atomRotation: [{
                id: 0,
                name: "YttriumRotation",
                timing: "250",
                spacing: "easeOutSine",
                rotationxstart: 0,
                rotationxfinal: 0,
                rotationystart: 0,
                rotationyfinal: 0,
                rotationzstart: 0,
                rotationzfinal: 45,
                atomid: 2,
                viewPortScaleX: 0.46875,
                viewPortScaleY: 0.46875
            }],
            atomOpacity: [{
                id: 0,
                name: "IndiumOpacity",
                timing: 250,
                spacing: "easeOutSine",
                opacitystart: 0,
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
                rotationzfinal: 0,
                widthstart: 50,
                heightstart: 50,
                widthfinal: 50,
                heightfinal: 50,
                translate: false,
                //translateYfinal: null,
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
                name: "MaltolMolecule",
                scaleId: 0,
                translateId: 0,
                translateDelay: 0,
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
                translateId: 0,
                translateDelay: 0,
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
                name: "SarkodinaOrganism",
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
            bestpracticeId: 0,
            bestid: 1,
            bestpracticeCollection:[],
            bestpractice:[{
              name: "TreeBestPractice",
              autoplay: false,
              click: false,
              id: 0,
              bestid: 1,
              firstElement: 0,
              secondElement: 0,
              thirdElement: 0,
              firstElementDelay: 0,
              secondElementDelay: 0,
              viewPortScaleX: 0.78125,
              viewPortScaleY: 0.78125
            }],
            bestpracticeNull:[{
              name: "-",
              autoplay: false,
              click: false,
              id: 0,
              bestid: 0,
              firstElement: 0,
              secondElement: 0,
              thirdElement: 0,
              firstElementDelay: 0,
              secondElementDelay: 0,
              viewPortScaleX: 0.78125,
              viewPortScaleY: 0.78125
            }],
            principleId: 0,
            principle:[{
              id: 0,
              name: "Flying",
              text: ""

            }],

            //
            randomElements: ['Hydrogen', 'Helium', 'Lithium', 'Beryllium', 'Boron', 'Carbon', 'Nitrogen', 'Oxygen', 'Fluorine', 'Neon', 'Sodium', 'Magnesium', 'Zinc', 'Krypton', 'Strontium', 'Niobium', 'Selenium'],
            randomMolecules: ['Acetone', 'Chromium ', 'Fluorite', 'Hexane', 'Jadeite', 'Niter', 'Picene', 'Tamoxifen', 'Topaz', 'Water', 'Zircon', 'Vanillin'],
            randomOrganisms: ['Cupulata', 'Mucorina', 'Astoma', 'Sporoza', 'Floridea', 'Diatomea', 'Bangialea', 'Fuciodea', 'Fungi', 'Exosporea', 'Heliozoa', 'Nuda'],
            randomBestpractice: ['Bee', 'Wasp', 'Spider', 'Fish', 'Beetle', 'Moth', 'Monkey', 'Butterfly', 'Plant', 'Snail', 'Shrew', 'Ant'],

        }
    },
    computed: {

        combineAtomCollection() {
            return this.atomCollection.concat(this.atomNull, this.atomTranslate, this.atomscale, this.atomRotation, this.atomOpacity)
        },
        combineMoleculeCollection() {
            return this.moleculeCollection.concat(this.moleculeNull, this.molecule)
        },
        combineOrganismCollection() {
            return this.moleculeCollection.concat(this.organismNull, this.organism)
        },
        combineBestpracticeCollection() {
            return this.bestpracticeCollection.concat(this.bestpracticeNull, this.bestpractice)
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
      addPrincipleCatOne() {
        this.principleId ++
              this.principle.push({
                id: this.principleId,
                name: "Flying",
                text: ""
              })
      },
      addBestPracticeCatOne() {
        this.bestpracticeId++,
            this.bestid++,
              this.bestpractice.push({
                name: this.randomBestpractice[Math.floor((Math.random() * 11) + 1)] + "Best",
                autoplay: false,
                click: false,
                id: this.bestpracticeId,
                bestid: this.bestid,
                firstElement: 0,
                secondElement: 0,
                thirdElement: 0,
                firstElementDelay: 0,
                secondElementDelay: 0,
                viewPortScaleX: 0.78125,
                viewPortScaleY: 0.78125
              })
      },
        addOrganismCatOne() {
            this.organismId++,
                this.orgid++,
                this.organism.push({
                    name: this.randomMolecules[Math.floor((Math.random() * 11) + 1)] + "Organism",
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
                    name: this.randomMolecules[Math.floor((Math.random() * 11) + 1)] + "Molecule",
                    translateId: 0,
                    translateDelay: 0,
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
                    name: this.randomElements[Math.floor((Math.random() * 11) + 1)] + "Scale",
                    timing: 250,
                    spacing: "easeOutSine",
                    widthstart: 50,
                    widthfinal: 200,
                    heightstart: 50,
                    heightfinal: 200,
                    atomid: this.atomId,
                    viewPortScaleX: this.atomViewPortScaleX,
                    viewPortScaleY: this.atomViewPortScaleY
                })
        },
        addatomtranslate() {
            this.atomId++,
                currentIdTranslate++,
                this.atomTranslate.push({
                    id: currentIdTranslate,
                    name: this.randomElements[Math.floor((Math.random() * 11) + 1)] + "Translate",
                    timing: 250,
                    spacing: "easeOutSine",
                    translate: true,
                    translateXstart: 50,
                    translateXfinal: 200,
                    translateYstart: 50,
                    translateYfinal: 200,
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
                    name: this.randomElements[Math.floor((Math.random() * 11) + 1)] + "Rotation",
                    timing: "250",
                    spacing: "easeOutSine",
                    rotationxstart: 0,
                    rotationxfinal: 0,
                    rotationystart: 0,
                    rotationyfinal: 0,
                    rotationzstart: 0,
                    rotationzfinal: 45,
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
                    name: this.randomElements[Math.floor((Math.random() * 11) + 1)] + "Opacity",
                    timing: 250,
                    spacing: "easeOutSine",
                    opacitystart: 0,
                    opacityfinal: 100,
                    atomid: this.atomId,
                    viewPortScaleX: this.atomViewPortScaleX,
                    viewPortScaleY: this.atomViewPortScaleY
                })
        }
    }
}
</script>

<style lang="sass">@import './scss/main.scss'</style>
