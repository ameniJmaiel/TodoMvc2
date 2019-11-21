<template>
  <div>
    <input id="toggle-all" class="toggle-all" v-model="status" type="checkbox">
    <label for="toggle-all">Mark all as complete</label>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: Boolean
    }
  },
  model: {
    event: 'checked'
  },
  computed: {
    status: {
      get () {
        return this.value
      },
      set (value) {
        this.$emit('checked', value)
      }
    }
  }
}
</script>