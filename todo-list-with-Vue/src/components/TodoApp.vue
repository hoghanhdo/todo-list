<template>
  <div class="container">
    <h1 class="text-center mt-5">Vue Todo App</h1>

    <!-- Task Input -->
    <div class="d-flex mt-5">
      <input
        v-model="task"
        type="text"
        placeholder="Write new task here"
        class="form-control"
      />
      <button class="btn btn-primary" @click="saveTask">Save</button>
    </div>

    <!-- Task List -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">Edit</th>
          <th scope="col" class="text-center">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <span
              :class="{
                completed: task.status === 'Completed',
              }"
              >{{ task.name }}</span
            >
          </td>
          <td>
            <span
              class="pointer"
              :class="{
                'text-danger': task.status === statuses[0],
                'text-warning': task.status === statuses[1],
                'text-success': task.status === statuses[2],
              }"
              @click="changeStatus(index)"
              >{{ task.status }}</span
            >
          </td>
          <td>
            <div class="text-center" @click="editTask(index)">
              <span class="fa fa-pen pointer"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "TodoApp",
  props: {
    msg: String,
  },
  data() {
    return {
      statuses: ["To-do", "In progress", "Completed"],
      task: "",
      editedTask: null,
      tasks: [
        {
          name: "Order a new light bulb",
          status: "To-do",
        },
        {
          name: "Pay electricity bill",
          status: "In progress",
        },
        {
          name: "Do groccery",
          status: "Completed",
        },
      ],
    };
  },
  methods: {
    saveTask() {
      if (this.task.length === 0) return;
      if (this.editedTask === null) {
        this.tasks.push({
          name: this.task,
          status: "To-do",
        });
      } else {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }
      this.task = "";
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },
  },
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
.completed {
  text-decoration: line-through;
}
</style>
