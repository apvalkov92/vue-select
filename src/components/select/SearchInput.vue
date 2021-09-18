<template>
  <div>
    <input @input="input($event.target.value)" :value="value" type="text">
  </div>
</template>

<script>
import Event from '../../enums/Event'

export default {
  name: 'SearchInput',
  props: {
    value: {
      type: String,
      required: true
    }
  },
  methods: {
    input (value) {
      this.$emit(Event.Input, value)
    }
  }
}
</script>

<style scoped>

</style>
