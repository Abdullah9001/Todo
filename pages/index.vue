<script setup>
import { useTodoStore } from "../store/todo";
const store = useTodoStore();
const computedTodos = computed(() => store.todos);

onMounted(() => {
  store.fetchAllPosts();
});
</script>

<template>
  <div class="h-full flex justify-center items-center bg-[#333]">
    <div class="h-screen pt-8">
      <div class="flex items-center justify-center">
        <div class="bg-white shadow-md rounded-lg border-2 p-3 w-full mt-10">
          <div class="header mb-16 text-center">
            <h1 class="text-3xl font-bold">Full-Stack Todo</h1>
          </div>
          <div class="main">
            <div class="input flex">
              <input
                type="text"
                placeholder="Insert your todo"
                class="input border-gray-900 border mr-3 w-80 h-10 rounded-md pl-3 outline-none"
                v-model="store.newTodo"
              />
              <button
                v-if="store.addButton"
                class="border-2 border-gray-900 p-1 font-sans bg-[#333] font-bold text-white text-sm rounded-md transition-all ease-in-out duration-700 hover:bg-slate-100 hover:text-slate-950"
                @click="store.addTodo()"
              >
                Submit
              </button>
              <button
                v-if="store.updateButton"
                class="border-2 border-gray-900 p-1 font-sans bg-[#333] font-bold text-white text-sm rounded-md transition-all ease-in-out duration-700 hover:bg-slate-100 hover:text-slate-950"
                @click="store.updateTodo()"
              >
                Update
              </button>
            </div>
            <p class="text-red-600 text-xs m-2 text-center justify-center">
              {{ store.errMsg }}
            </p>
          </div>
          <div class="mt-4 p-3 rounded-lg border border-gray-600">
            <div class="list-text">
              <h1 class="text-2xl font-bold font-sans text-slate-950">
                Todo Item
              </h1>
            </div>
            <div
              class="todo-list"
              v-for="todo in computedTodos"
              :key="todo._id"
            >
              <div
                class="flex justify-between items-center border border-gray-500 rounded-lg p-2 mt-3"
              >
                <div class="items">
                  <p
                    class="font-xl text-lg font-sans font-bold text-slate-500"
                    :style="{ color: todo.color }"
                  >
                    {{ todo.todo }}
                  </p>
                </div>
                <div class="button">
                  <button
                    class="border border-green-500 mr-2 font-sans text-slate-500 font-bold p-1 text-xs rounded"
                    @click="store.editTodo(todo._id, todo)"
                  >
                    Edit
                  </button>
                  <button
                    class="border border-red-500 mr-2 text-xs text-slate-500 font-sans font-bold p-1 rounded"
                    @click="store.deleteTodo(todo._id)"
                  >
                    Delete
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
