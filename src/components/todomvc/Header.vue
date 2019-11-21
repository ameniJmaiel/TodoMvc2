<template>
  <header class="header">
    <h1>todos</h1>
    <input class="new-todo" v-model.trim="newTodo" @keyup.enter="save" autofocus autocomplete="off" placeholder="What needs to be done?">
  </header>  
</template>

<script>
export default {
  data () {
    return {
      newTodo: ''
    }
  },
  methods: {
    save: function () {
      if (this.newTodo.length) {
        this.$emit('save', {
          id: Date.now(),
          name: this.newTodo,
          completed: false
        })
      }
      this.newTodo = ''
    }
  }
}
</script>