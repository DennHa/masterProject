<template name="molecule">
<div class="molecule__bond">
    <div class="molecule__viewer">
        <transition v-on:before-enter="beforeEnter" v-on:enter="enter" v-on:leave="leave" v-bind:css="false">
            <div class="molecule__nukleolus" v-if="nukleolus"></div>
        </transition>
    </div>

    <div class="molecule__properties">
      <form class="" action="index.html" method="post" >
        <input name="name"   class="atom__name">
      </form>
      <div>
        <select class="atom__kind" v-model="selected">
           <option v-for="atom in atoms" value="atom.atomid" >
             {{ atom.name }}
           </option>
        </select>
        <select  class="atom__kind">
           <option v-for="atom in atoms">
             {{ atom.name }}
           </option>
        </select>
        <select  class="atom__kind">
           <option v-for="atom in atoms">
             {{ atom.name }}
           </option>
        </select>
        <select  class="atom__kind">
           <option v-for="atom in atoms">
             {{ atom.name }}
           </option>
        </select>
    </div>


        <div class="molecule__timing">
            <!-- <form>
                <input name="time" v-model="value[id].timing" value="" type="number">
                <select v-model="value[id].spacing" class="atom__kind">
                   <option v-for="ease in easings" v-bind:value="ease.easeFunction"  >
                     {{ ease.easeFunction }}
                   </option>
              </select>
            </form> -->
        </div>
    </div>
</div>
</template>
<script>

export default {
    name: "molecule",

    props: ['atomCollection'],
    data() {
        return {
            nukleolus: true,
            selected: "",
            value: ""
        }
    },
    mounted: function() {
      this.nukleolus = false

    },
    updated(){

    },
    computed: {
      atoms(){
        return this.atomCollection.sort(function (a, b) {
          if (a.atomid > b.atomid) {
            return 1
          }
          if (a.atomid < b.atomid) {
            return -1
          }
          // a must be equal to b
          0
        })
      },
      currentid(){
        return this.selected
      }
    },

    methods: {

        //before animation
        beforeEnter: function(el) {
            el.style.width = this.atomWidthStart + "%",
            el.style.height = this.atomHeightStart + "%"
        },

        //animation enter
        enter: function(el, done) {
            var vm = this
            Velocity(el, {
                width: "20%",
                height: "20%"
            }, {
                //delay: "2000",
                easing: this.spacing,
                duration: this.atomDuration,
                complete: function() {
                    done()
                    if (!vm.stop) vm.nukleolus = false

                }
            })

        },

        //animation leave - just for restart
        leave: function(el, done) {
            var vm = this
            Velocity(el, {
                backgroundColor: '#ffffff',
            }, {
                duration: 1,
                delay: "2000",
                complete: function() {
                    done()
                    vm.nukleolus = true
                }
            })
        }
    },

}
</script>
