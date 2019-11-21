<template>
  <div id="todomvc">
		<section class="todoapp">
		<todo-header @save="todos.push($event)"></todo-header>
			<section class="main">
				<toggle-all v-model="toggleAll"></toggle-all>
				<todos :filtered-todos="filteredTodos" @delete="deleteByID"></todos>
			</section>
			<footer class="footer">
				<todo-count :nb="activeTodos.length"></todo-count>
				<todo-filters :current.sync="currentFilter" :filters="filters"></todo-filters>
				<button v-show="completedTodos.length" @click="todos = activeTodos" class="clear-completed">
					Clear completed
				</button>
			</footer>
		</section>
		<footer class="info">
			<p>Double-click to edit a todo</p>
		</footer>
	</div>
</template>
<script>
import toggleAll from "@/components/todomvc/ToggleAll"
import todos from "@/components/todomvc/Todos"
import todoHeader from "@/components/todomvc/Header"
import todoCount from "@/components/todomvc/Count"
import todoFilters from "@/components/todomvc/Filters"

export default {
  components: {
    toggleAll,
    todos,
    todoHeader,
    todoCount,
    todoFilters
  },
  data () {
    return {
      filters: ['all', 'active', 'completed'],
      currentFilter: 'all',
      todos: []
    }
  },
  computed: {
    toggleAll: {
      get () {
        return !this.activeTodos.length
      },
      set (value) {
        this.todos.forEach((todo) => {
          todo.completed = value
        })
      }
    },
    filteredTodos: function () {
      if (this.currentFilter === 'active') {
        return this.activeTodos
      } else if (this.currentFilter === 'completed') {
        return this.completedTodos
      } else {
        return this.todos
      }
    },
    activeTodos: function () {
      return this.todos.filter(function (todo) {
        return !todo.completed
      })
    },
    completedTodos: function () {
      return this.todos.filter(function (todo) {
        return todo.completed
      })
    }
  },
  methods: {
    deleteByID: function (id) {
      this.todos = this.todos.filter(function (todo) {
        return todo.id !== id
      })
    }
  }
}
</script>
