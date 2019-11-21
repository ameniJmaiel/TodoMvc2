<template>
  <ul class="todo-list">
    <li class="todo" v-for="todo in filteredTodos" :key="todo.id" :class="{completed: todo.completed, editing: copiedTodo && copiedTodo.id === todo.id}">
      <div class="view">
        <input class="toggle" v-model="todo.completed" type="checkbox">
        <label @dblclick="copiedTodo = Object.assign({}, todo)">{{ todo.name }}</label>
        <button class="destroy" @click="$emit('delete', todo.id)"></button>
      </div>
      <input class="edit" v-focus="copiedTodo && copiedTodo.id === todo.id" v-model.trim="todo.name" @keyup.esc="cancel(todo)" @keyup.enter="edit(todo)" @blur="edit(todo)" type="text"/>
    </li>
  </ul>
</template>

<script>
export default {
  props: {
    filteredTodos: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      copiedTodo: null
    }
  },
  methods: {
    cancel: function (todo) {
      todo.name = this.copiedTodo.name
      this.copiedTodo = null
    },
    edit: function (todo) {
      if (!todo.name.length) {
        this.$emit('delete', todo.id)
      }
      this.copiedTodo = null
    }
  },
  directives: {
    focus: {
      // dÃ©finition de la directive
      update: function (el, binding) {
        if (binding.value) {
          el.focus()
        }
      }
    }
  }
}
</script>