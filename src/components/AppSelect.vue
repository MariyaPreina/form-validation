<template>
  <div class="select">
    <p
      class="select__value"
      :class="{active: areOptionsVisible, 'not-selected': !selected}"
      @click="areOptionsVisible = !areOptionsVisible"
    >{{ isSelected }}</p>
    <div class="select__options" v-if="areOptionsVisible">
      <span
        class="select__option"
        v-for="option in options"
        :key="option.value"
        @click="selectOption(option)"
      >{{ option.name }}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    options: {
      type: Array,
      default () {
        return []
      }
    },
    default: {
      type: String,
      required: false,
      default: ''
    },
    selected: {
      type: String,
      default: ''
    }
  },
  data () {
    return {
      areOptionsVisible: false
    }
  },
  computed: {
    isSelected () {
      return this.selected ? this.selected : this.default
    }
  },
  methods: {
    hideSelect (e) {
      if (!this.$el.contains(e.target)) {
        this.areOptionsVisible = false
      }
    },
    selectOption (option) {
      this.$emit('select', option)
      this.areOptionsVisible = false
    }
  },
  mounted () {
    document.addEventListener('click', this.hideSelect)
  },
  beforeUnmount () {
    document.removeEventListener('click', this.hideSelect)
  }
}
</script>
