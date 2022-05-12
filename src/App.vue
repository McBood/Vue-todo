<template>
  <h3>Today Tasks</h3>
  <div class="tasks">
    <div
      class="task"
      :class="{ completed: task.isCompleted }"
      v-for="task in tasks"
      :key="task.id"
      @click="completedChange(task.id)"
    >
      <div
        class="round"
        :class="{
          business: task.type === 'business',
          personal: task.type === 'personal',
        }"
      ></div>
      <span :class="{ completed: task.isCompleted }">{{ task.name }}</span>
      <button @click="delTask(task.id)" class="btnDel">Delete</button>
    </div>
  </div>

  <div class="add-task">
    <input type="text" placeholder="Name of task" v-model="taskName" />
    <button @click="addTask" class="btnAdd">Add</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      taskName: "",
      tasks: [
        {
          id: "2132145123124",
          name: "Create todo",
          isCompleted: false,
          type: "business",
        },
      ],
    };
  },
  methods: {
    completedChange: function (taskId) {
      const currentTask = this.tasks.find((t) => t.id === taskId);
      currentTask.isCompleted = !currentTask.isCompleted;
    },
    addTask: function () {
      if (this.taskName) {
        this.tasks.push({
          id: Math.random().toString(36).substring(2, 7),
          name: this.taskName,
          type: "personalz",
          isCompleted: false,
        });
        this.taskName = "";
      }
    },
    delTask: function (taskId) {
      this.tasks = this.tasks.filter((t) => t.id != taskId);
    },
  },
};
</script>
