<template name="atomProperty">
      <span>
        {{this.prefix}}

        <input v-if="acceptType == 'number'" :atom-property="value" type="number" v-model="proptery"  @input="$emit('input', $event.target.value)"/>
        <input v-if="acceptType == 'color'" :atom-property="color" type="color" v-model="proptery"  @input="$emit('input', $event.target.value)"/>
        {{this.unit}}
        <input v-if="acceptType == 'all'" :atom-property="value"  v-model="proptery"  @input="$emit('input', $event.target.value)"/>
        <input style="display:none;"></form>
      </span>
</template>

<script>
export default {
  name: 'atomProperty',
  props: ['value', 'prefix', 'unit', 'acceptType', 'nameElement'],
  data () {
    return {
      proptery: "",

    }
  },
  created: function() {
      this.proptery = this.value
  },
  beforeUpdate: function() {
      this.proptery = this.value

  },
  computed: {
  }

}
</script>
