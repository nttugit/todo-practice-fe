<template>
  <div class="container">
    <div class="task">
      <div class="title"><h1>To Do List</h1></div>
      <div class="form">
        <search-bar v-model="searchedKeyword" @search="searchByName" />
      </div>
      <div class="form">
        <input
          type="text"
          placeholder="New task"
          v-model="newTask"
          @keyup.enter="addTask"
        />
        <button @click="addTask"><i class="fas fa-plus"></i></button>
      </div>
      <div class="task-items">
        <ul>
          <task-item
            v-bind:task="task"
            v-for="(task, index) in filteredTasks"
            :key="index"
            @remove="removeTask(task.id)"
            @complete="completeTask(task)"
          ></task-item>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import SearchBar from "./SearchBar.vue";
import TaskItem from "./TaskItem.vue";
export default {
  name: "TodoApp",
  components: {
    SearchBar,
    TaskItem,
  },
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: "Learn Vue JS",
          completed: true,
        },
        {
          id: 2,
          title: "Watch netflix",
          completed: true,
        },
        {
          id: 3,
          title: "Go shopping",
          completed: false,
        },
        {
          id: 4,
          title: "Learn guitar",
          completed: false,
        },
        {
          id: 5,
          title: "Send email",
          completed: false,
        },
      ],
      nextTaskId: 6,
      searchedKeyword: "",
      newTask: "",
    };
  },
  mounted() {
    this.loadTodoListFromLocalStorage();
  },
  methods: {
    loadTodoListFromLocalStorage() {
      this.tasks = JSON.parse(localStorage.getItem("todos")) || [];
    },
    saveTodoListIntoLocalStorage() {
      localStorage.setItem("todos", JSON.stringify(this.tasks));
    },
    searchByName(searchedKeyword) {
      console.log(searchedKeyword);
    },
    addTask() {
      if (this.newTask) {
        this.tasks.unshift({
          id: this.nextTaskId,
          title: this.newTask,
          completed: false,
        });
        this.newTask = "";
        this.nextTaskId++;
      }
      // localStorage.setItem("todos", JSON.stringify(this.tasks));
      this.saveTodoListIntoLocalStorage();
    },
    removeTask(id) {
      this.tasks = this.tasks.filter((t) => t.id !== id);
      this.saveTodoListIntoLocalStorage();
    },
    completeTask(task) {
      task.completed = !task.completed;
      this.saveTodoListIntoLocalStorage();
    },
  },
  computed: {
    filteredTasks() {
      if (this.searchedKeyword) {
        return this.tasks.filter((t) =>
          t.title.toLowerCase().includes(this.searchedKeyword.toLowerCase())
        );
      } else {
        return this.tasks;
      }
    },
  },
};
</script>

<style></style>
