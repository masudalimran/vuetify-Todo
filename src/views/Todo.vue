<template>
  <div class="home">
    <v-text-field
      class="pa-3"
      label="Add Task"
      placeholder="Add Your Task Title"
      outlined
      append-icon="mdi-plus"
      hide-details
      clearable
      v-model="newTaskTitle"
      @click:append="addTask"
      @keyup.enter="addTask"
    ></v-text-field>
    <v-list flat class="pt-0 mt-0">
      <div v-for="task in tasks" :key="task.id">
        <v-list-item
          @click="doneTask(task.id)"
          :class="{ 'green lighten-4 ': task.done }"
        >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title
                :class="{ 'text-decoration-line-through': task.done }"
              >{{ task.title }}</v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn icon @click.stop="deleteTask(task.id)">
                <v-icon color="red lighten-1 ">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
        <v-divider></v-divider>
      </div>
    </v-list>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
      newTaskTitle: '',
      taskId: 0
    };
  },
  methods: {
    doneTask(id) {
      // console.log('Id', id)
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id != id);
    },
    addTask(){
      console.log(this.taskId , this.newTaskTitle)
      let newTask = {
        id: this.taskId,
        title: this.newTaskTitle,
        done: false
      }
      this.tasks.push(newTask)
      this.taskId++
      this.newTaskTitle = ''
    },
  },
};
</script>
