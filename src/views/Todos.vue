<template>
  <div>
    
    <h2>Список Задач:</h2>
    <hr>
    <AddTodo 
      @add-todo="addTodo"
    />
    <select v-model="filter">
      <option value="all">Все</option>
      <option value="completed">Выполненные</option>
      <option value="not-completed">Активные</option>
    </select>
    <hr>
    <TodoList 
      v-if="filteredTodos.length"
      :todos="filteredTodos"
      @remove-todo="removeTodo"
    />
    <p v-else>Нет задач!</p>

    <router-link to="/">Назад</router-link>
    
  </div>
</template>

<script>
import TodoList from '../components/TodoList'
import AddTodo from '../components/AddTodo'
export default {
  name: 'app',
  data() {
    return {
      todos: [],
      filter: 'all'
    }
  },
  components: {
    TodoList,
    AddTodo
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  computed: {
    filteredTodos() {
      let filter
      if (this.filter === 'all') {
        return this.todos
      }

      if (this.filter === 'completed') {
        return this.todos.filter(t => t.completed)
      }

      if (this.filter === 'not-completed') {
        return this.todos.filter(t => !t.completed)
      }

      return filter
    }
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todos"))
  },
  watch: {
    todos (newValue) {
      localStorage.setItem("todos", JSON.stringify(newValue));
    }
  }
}
</script>

<style scoped>
  select {
    margin-top: 10px;
    margin-left: 180px;
  }
</style>
