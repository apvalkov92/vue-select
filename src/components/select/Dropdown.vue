<template>
  <div>
    <ul>
      <li
        v-for="(option, index) in options"
        @click.prevent="click(option)"
        :key="index"
        :class="{ selected: isSelected(option) }"
      >
        <a>
          {{ option }}
        </a>
      </li>
    </ul>
    <br>
  </div>
</template>

<script>
import Event from '../../enums/Event'

export default {
  name: 'Dropdown',
  props: {
    options: {
      type: Array,
      required: true
    },
    selectedOptions: {
      required: true
    }
  },
  methods: {
    isSelected (option) {
      return this.selectedOptions instanceof Array
          ? this.selectedOptions.filter(selectedOption => selectedOption === option).length > 0
          : this.selectedOptions === option
    },
    click (option) {
      this.$emit(Event.Click, option)
    }
  }
}
</script>

<style scoped>
li {
  cursor: pointer;
}

.selected {
  background-color: darkgrey;
}
</style>
