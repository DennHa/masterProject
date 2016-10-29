<template name="atomProperty">

        <input :atom-duration="value" v-model="proptery"  @input="$emit('input', $event.target.value)"  />

</template>

<script>
export default {
  name: 'atomProperty',
  props: ['value'],
  data () {
    return {
      proptery: "",
    }
  },
  created: function() {
      this.proptery = this.value
  },


}
</script>
