<template>
<section class="universe">
	<atom></atom>
	<atom></atom>
</section>
</template>

<script>
import atom from './components/atoms/atom.vue'

export default {
  name: 'universe',
  components: {
    atom
  }
}

</script>

<style lang="sass">
@import './scss/main.scss';
</style>


