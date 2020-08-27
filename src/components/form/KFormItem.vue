<template>
  <div>
    <h3>KFormItem</h3>
    <label v-if="label">{{label}}</label>
    <slot></slot>  
    <div v-if="error" class="error">{{error}}</div>
  </div>
</template>

<script>
  import Schema from 'async-validator'
  export default {
    name: 'KFromItem',
    inject: {
      form: 'form'
    },
    props: {
      label: {
        type: String,
        default: ''
      },
      prop: {
        type: String,
        default: ''
      }
    },
    data () {
      return {
        error: ''
      }
    },
    methods: {
      validate () {
        const rules = this.form.rules[this.prop]
        const value = this.form.model[this.prop]
        const schema  = new Schema({[this.prop]: rules})
        return schema.validate({[this.prop]: value}, (errors) => {
          if (errors) {
            this.error = errors[0].message
          } else {
            this.error = ''
          }
        })

      }
    }
  }
</script>

<style lang="scss" scoped>

</style>