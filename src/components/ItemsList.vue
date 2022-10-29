<template>
  <main>
    <div class="add-new-div">
      <input
        class="add-new-input"
        type="text"
        placeholder="Create a new todo...."
        v-model="newItem"
        @keyup.enter="setItem"
      />
    </div>
    <section class="items-list">
      <div class="empty" v-if="todos.length == 0">
        <p>Todos List currently is empty, please start to add some...</p>
      </div>
      <div class="item" v-for="todo in UITodos" :key="todo.id">
        <label class="item-label">
          <input type="checkbox" id="checkbox" v-model="todo.completed" />
          <p>{{ todo.title }}</p>
          <span class="checkmark"></span>
        </label>
        <button class="remove" @click="removeTodo(todo.id)">
          <img src="../assets/icon-cross.svg" alt="remove" />
        </button>
      </div>
      <items-footer
        :counter="counter"
        @set="updateUI"
        @clearCompleted="clearCompleted"
      ></items-footer>
    </section>
  </main>
</template>

<script>
import ItemsFooter from "./ItemsFooter.vue";

export default {
  components: { ItemsFooter },
  data() {
    return {
      newItem: "",
      itemId: Math.floor(Math.random() * 100),
      counter: 2,
      todos: [],
      UITodos: [],
      activeTodos: [],
      completedTodos: [],
    };
  },

  watch: {
    UITodos: {
      handler() {
        localStorage.setItem("todosRef", JSON.stringify(this.todos));

        let activeTodos = this.todos.filter((t) => !t.completed);
        let completedTodos = this.todos.filter((t) => t.completed);

        localStorage.setItem("active-todos", JSON.stringify(activeTodos));
        localStorage.setItem("completed-todos", JSON.stringify(completedTodos));

        this.counter = activeTodos.length;
        this.activeTodos = activeTodos;
        this.completedTodos = completedTodos;
      },
      deep: true,
    },
  },

  methods: {
    setItem() {
      let newItem = {
        title: this.newItem,
        completed: false,
        id: this.itemId++,
      };
      if (this.newItem.trim() === "") {
        confirm("please fill the input");
        return;
      }
      this.todos.unshift(newItem);
      this.UITodos = this.todos;
      this.newItem = "";
    },
    removeTodo(todoId) {
      if (confirm("Are You Sure ?")) {
        this.todos = this.todos.filter((res) => res.id !== todoId);
        this.UITodos = this.UITodos.filter((res) => res.id !== todoId);
      }
    },
    updateUI(selected) {
      if (selected === "all") {
        this.UITodos = this.todos;
      }
      if (selected === "active") {
        this.UITodos = this.activeTodos;
      }
      if (selected === "checked") {
        this.UITodos = this.completedTodos;
      }
    },
    clearCompleted() {
      if (this.completedTodos.length == 0) {
        confirm("there is no completed Todos!");
      } else if (confirm("Delete all completed Todos ?")) {
        localStorage.removeItem("completed-todos");
        this.todos = this.activeTodos;
      }
      this.UITodos = this.activeTodos;
    },
  },

  mounted() {
    this.todos = JSON.parse(localStorage.getItem("todosRef")) || this.todos;
    this.activeTodos = JSON.parse(localStorage.getItem("active-todos"));
    this.completedTodos =
      JSON.parse(localStorage.getItem("completed-todos")) || this.todos;
    this.UITodos = this.todos;
  },
};
</script>
