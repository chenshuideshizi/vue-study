<template>
  <input 
    :type="type" 
    :value="value"
    v-bind="$attrs"
    @input="onInput"
  >
</template>

<script>
  export default {
    name: 'KInput',
    props: {
      value: {
        type: String,
        default: ''
      },
      type: {
        type: String,
        default: 'text'
      }
    },
    methods: {
      onInput (e) {
        this.$emit('input', e.target.value)
        
        this.$parent.validate()
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>