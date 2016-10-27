<template name="atom">
    <div class="atom__shell">
      <form class="atom__name" v-on:submit.prevent>
        <input type="" name="atome_nameChange" v-model="atomName" placeholder="Name"/>
        <input type="text" style="display:none;">
      </form>
      <div class="atom__viewer">
        <transition
          v-on:before-enter="beforeEnter"
          v-on:enter="enter"
          v-on:leave="leave"
          v-bind:css="false"
        >
          <div class="atom__nukleolus" v-if="nukleolus"></div>
         </transition>

      </div>
      <div class="atom__properties">
      <form class="atom__behavior">
        <div class="atom__kind">
          <option v-for="option in options" :value="option.value" />
        </div>
        <div class="atom__timing">
          <h3> timing </h3>
          <input type="number" v-model="atomDuration" />
          <input type="number" v-model="atomDelay">
        </div>
        <div class="atom__characteristics">
         <h3>characteristics</h3>
         <input type="number" v-model="atomWidth" />
         <input type="number" v-model="atomHeight">
        </div>
      </form>

      </div>
    </div>
</template>

<script>
import atomTiming from './atom-timing.vue'



  export default {
    name: "atom",
    components: {
      atomTiming
    },

    data () {
      return{
        atomName: "",
        atomWidth: "20",
        atomHeight: "20",
        nukleolus: true,
        duration: 1000

      }
    },
    mounted: function () {
      this.nukleolus = false
    },
    
    methods: {

      beforeEnter: function (el) {
        el.style.width = '2vw'
        el.style.height = '2vw'
    },
      enter: function (el, done) {
        var vm = this
        Velocity(el,
          { width: this.atomWidth,
           height: this.atomHeight ,
           translateX: "200px"
          },
          {
           easing: "easeInSine",
            duration: this.duration,
            complete: function () {
              done()
              if (!vm.stop) vm.nukleolus = false
            }
          }
        )
      },
      leave: function (el, done) {
        var vm = this
        Velocity(el,
          { width: '2vw',
            height: '2vw' },
          {
            duration: this.duration,
            complete: function () {
              done()
              vm.nukleolus = true
            }
          }
        )
      }
    }
  }
</script>
