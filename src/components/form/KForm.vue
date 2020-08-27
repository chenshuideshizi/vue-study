<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
  export default {
    name: 'KFrom',
    provide () {
      return {
        form: this
      }
    },
    props: {
      model: {
        type: Object,
        default: () => ({})
      },
      rules: {
        type: Object,
        default: () => ({})
      }
    },
    methods: {
      validate (cb) {
        const tasks = this.$children.filter(item => item.prop).map(item => item.validate())
        console.log('tasks', tasks)
        Promise.all(tasks)
          .then(() => cb(true))
          .catch(() => cb(false))
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>