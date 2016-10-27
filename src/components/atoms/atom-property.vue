<template name="atomProperty">

        <input :atom-duration="value" v-model="duration"  @input="$emit('input', $event.target.value)"  type="number" />

</template>

<script>
export default {
  name: 'atomProperty',
  props: ['value'],
  data () {
    return {
      duration: ""
    }
  },
  created: function() {
      this.duration = this.value
  }

}
</script>
