<template>
  <h1 class="py-4 text-3xl font-semibold">todo example lol</h1>
  <div class="flex h-full flex-col items-center justify-between px-4">
    <div class="mb-4 flex w-full max-w-xl" style="backface-visibility: hidden">
      <input
        v-model="newTodoField"
        type="text"
        class="mr-4 flex-grow rounded-md bg-gray-300 px-4 py-2 text-xl shadow-md outline-none ring-red-500 transition-all focus:scale-[102%] focus:shadow-lg focus:ring-2"
        placeholder="Add a new todo :)"
        @keydown.enter="addToTodo"
      />
      <button
        class="rounded-full bg-red-500 py-2 px-4 text-xl font-semibold text-white shadow-md transition-all hover:-translate-y-1 hover:shadow-lg"
        @click="addToTodo"
      >
        <fa-icon :icon="['fas', 'plus']" class="text-xl active:bg-red-900" />
        Add
      </button>
    </div>
    <div class="flex w-full max-w-xl flex-col-reverse gap-y-2">
      <todo-item
        v-for="(todo, i) in todos"
        :key="todo"
        :todo="todo"
        @remove="removeFromTodo(i)"
      />
    </div>
  </div>
</template>

<script lang="ts">
  import { defineComponent } from "vue";
  import TodoItem from "./components/TodoItem.vue";

  export default defineComponent({
    components: {
      TodoItem,
    },
    data() {
      return {
        newTodoField: "",
        todos: [],
      };
    },
    methods: {
      addToTodo() {
        if (this.newTodoField == "") return;

        // @ts-ignore
        this.todos.push(this.newTodoField);
        this.newTodoField = "";
      },
      removeFromTodo(index: number) {
        this.todos.splice(index, 1);
      },
    },
  });
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #000;
  }
</style>
