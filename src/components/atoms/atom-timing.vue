<template name="atomTiming">
	<div class="atom__timing">
			<h3>Timing:</h3>
			<div class="atom__duration" v-on:submit.prevent >
				<span>Duration:</span>
				<input v-model="fadeDuration" @keyup.enter="saveNumber" type="number" placeholder="1000ms" />
				<input type="text" style="display:none;">
			</div>
	</div>
</template>

<script>
export default {
  name: 'atomTiming',
  data () {
    return {
      fadeDuration: "",
    }
  },
		methods:{
			saveNumber: function(){
				console.log(this.fadeDuration)
				this.$emit("this.fadeDuration")
				this.saveNumber = ""
			}
		}
}
</script>
