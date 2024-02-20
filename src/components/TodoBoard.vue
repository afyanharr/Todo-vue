<template>
   <section class="vh-100">
        <div class="container py-5 h-100">
            <div class="row d-flex justify-content-center align-items-center h-100">
                <div class="card" id="list1" style = "border-radius: .75rem; background-color: #eff1f2;">
                    <div class="card-body py-4 px-4 px-md-5">

                      <p class="h1 text-center mt-3 mb-4 pb-3 text-primary">
                        <u>My Todo</u>
                      </p>

                      <div class="card pb-2">
                        <form @submit.prevent="addNewTodo">
                          <input type="text" v-model="newTodoText" placeholder="Enter your todo..." />
                          <input type="date" id="date" v-model="selectedDate">
                          <button class="btn btn-primary" type="submit">Add Todo</button>
                        </form>
                        <TodoItems :todos="todos" @deleteTodo="deleteTodo" @changeStatusTodo="changeStatusTodo" />
                      </div>
                    </div>
                </div>
            </div>
        </div>
    </section>    
  </template>
  
  <script>
  import TodoItems from "./TodoItems.vue";
  
  export default {
    name: "TodoBoard",
    components: {
      TodoItems,
    },
    props: ["todos"],
    data() {
      return {
        selectedDate: null,
        newTodoText: "",
      };
    },
    methods: {
      addNewTodo() {
        if (this.newTodoText.trim() !== "") {
          const createdDate = new Date(Date.now());

          const newTodo = {
            id: Date.now(),
            createdWhen: createdDate.toISOString().split('T')[0],
            text: this.newTodoText,
            completed: false,
            deadline: this.selectedDate
          };
          this.$emit("addTodo", newTodo);
          this.newTodoText = "";
        }
      },
      deleteTodo(todoId) {
        this.$emit("deleteTodo", todoId);
      },
      changeStatusTodo(todoId) {
        this.$emit("changeStatusTodo", todoId);
      },
    },
  };
  </script>

<style>

</style>
  