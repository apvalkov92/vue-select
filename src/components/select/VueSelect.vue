<template>
  <div>
    <p>
      {{ value | selected }}
    </p>
    <search-input v-model="search" />
    <dropdown @click="clickOption" :options="filteredOptions" :selected-options="internalValue" />
  </div>
</template>

<script>
import SearchInput from './SearchInput'
import Dropdown from './Dropdown'
import Event from '../../enums/Event'

export default {
  name: 'VueSelect',
  components: {
    SearchInput,
    Dropdown
  },
  props: {
    value: {
      required: true
    },
    options: {
      type: Array,
      required: true
    },
    multiple: {
      type: Boolean,
      default: false
    }
  },
  filters: {
    selected (value) {
      return value instanceof Array ? value.join(',') : value
    }
  },
  data () {
    return {
      search: '',
      selected: null,
      selectedMultiple: []
    }
  },
  computed: {
    filteredOptions () {
      if (this.search === '') {
        return this.options
      }

      return this.options.filter(option => option.includes(this.search))
    },
    internalValue: {
      get () {
        return this.multiple ? this.selectedMultiple : this.selected
      },
      set (value) {
        if (this.multiple) {
          value instanceof Array ? this.selectedMultiple = value : this.selectedMultiple.push(value)
        } else {
          this.selected = value
        }
      }
    }
  },
  mounted () {
    this.internalValue = this.value
  },
  methods: {
    clickOption (option) {
      this.isSelectedOption(option) ? this.unselect(option) : this.select(option)
    },
    select (option) {
      this.internalValue = option

      this.input(this.internalValue)
    },
    unselect (unselectOption) {
      const index = this.selectedMultiple.findIndex(option => unselectOption === option)

      if (!this.multiple || index < 0) {
        return
      }

      this.selectedMultiple.splice(index, 1)

      this.input(this.internalValue)
    },
    input (value) {
      this.$emit(Event.Input, value)
    },
    isSelectedOption (selectedOption) {
      if (this.multiple) {
        return this.selectedMultiple.filter(option => option === selectedOption).length > 0
      }

      return selectedOption === this.selected
    }
  }
}
</script>
