<template>
  <div class="container has-background-grey-lighter p-2">
      <div class="columns mt-2">
        <div class="column is-6">
          <button class="button is-success mb-2" @click="addingTask = true">
            Add new Task
          </button>
          <TaskList :tasks="tasks" @remove-task="removeTask"/>
        </div>
        <div class="column is-6" v-if="addingTask">
          <AddTask :id="lastId" @add-task="addTask"/>
        </div>
      </div>
  </div>
</template>

<script>
import TaskList from "./components/TaskList.vue";
import AddTask from "./components/AddTask.vue";

export default {
    name: "App",
    data() {
        return {
            tasks: [],
            addingTask: false,
            lastId: 1,
        };
    },
    components: { TaskList, AddTask },
    methods: {
      addTask(task){
        const startDate = new Date(task.startDate);
        const endDate = new Date(task.endDate);

        if(startDate > endDate){
          alert('End date cannot be earlier than start date!')
          return;
        }

        this.tasks.push(task);
        this.lastId++;
        this.addingTask = false;
      },
      removeTask(id){
        this.tasks = this.tasks.filter(task => task.id !== id);
      }
    }
}
</script>