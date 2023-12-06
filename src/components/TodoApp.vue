<template>
    <div class="container">
      <h2 class="text-center mt5">Altschool Vue Todo App Assignment</h2>
  
      <!-- input -->
      <div class="d-flex">
        <input
          v-model="task"
          type="text"
          placeholder="Enter task"
          class="form-control"
        />
        <button @click="submitTask" class="btn btn-warning rounded-0">
          SUBMIT
        </button>
      </div>
  
      <!-- Task table  -->
      <table class="table table-bordered mt-5">
        <thead>
          <tr>
            <th scope="col">Task</th>
            <th scope="col">Status</th>
            <th scope="col" class="text-center">#</th>
            <th scope="col" class="text-center">#</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td>{{ task.name }}</td>
            <td>{{ task.status }}</td>
            <td>
              <div class="text-center" @click="editTask(index)">
                <span class="fa fa-pen"></span>
              </div>
            </td>
            <td>
              <div class="text-center" @click="deleteTask(index)">
                <span class="fa fa-trash"></span>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        task: "",
        editedTask: null,
        tasks: [
          {
            name: "Work out my assignment",
            status: "To-do",
          },
          {
            name: "Lose 10kg in 2 months",
            status: "In progress",
          },
        ],
      };
    },
  
    methods: {
      submitTask() {
        if (this.task === "") return;
        if (this.editedTask !== null) {
          this.tasks[this.editedTask].name = this.task;
          this.editedTask = null;
          this.task = "";
          return;
        }
        this.tasks.push({
          name: this.task,
          status: "To-do",
        });
        this.task = "";
      },
      deleteTask(index) {
        this.tasks.splice(index, 1);
      },
      editTask(index) {
        this.task = this.tasks[index].name;
        this.editedTask = index;
      },
    },
  };
  </script>
  