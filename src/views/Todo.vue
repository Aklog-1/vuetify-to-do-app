<template>
  <div class="home">
    
    <v-text-field
      v-model="newTaskTitle"
      @click:append="addTask"
      @keyup.enter = "addTask"
      class="pa-3"
      outlined
      label="Add task"
      append-icon="mdi-plus"
      hide-details
      clearable
      >
    </v-text-field>

  <v-list
      flat
      class="pt-0"
    >

    <div
    v-for= "task in tasks"
    :key="task.id">
      
      <v-list-item
      @click= "doneTask(task.id)"
      :class="{'blue lighten-5' : task.done}"
      >
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content
            :class="{'text-decoration-line-through' : task.done}"
            >
              <v-list-item-title>{{task.title}}</v-list-item-title>
            </v-list-item-content>

          <v-list-item-action>
          <v-btn 
          @click.stop = "deleteTask(task.id)"
          icon>
            <v-icon color="primary">mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
          </template>
          <v-divider></v-divider>
        </v-list-item>
        <v-divider></v-divider>
    </div>
        

    </v-list>

  </div>
</template>

<script>

  export default {
    name: 'Home',
    data() {
      return {
        newTaskTitle: "",
        tasks: [
          // {
          //   id: 1,
          //   title: "wake up",
          //   done: false
          // },
          // {
          //   id: 2,
          //   title: "brush ur teeth",
          //   done: false
          // },
          // {
          //   id: 3,
          //   title: "breakfast",
          //   done: true
          // },
          // {
          //   id: 4,
          //   title: "go to school",
          //   done: false
          // },
        ]
      }
    },
    methods: {
      addTask() {
        let newTask = {
          id: Date.now(),
          title: this.newTaskTitle,
          done: false
        }
        this.tasks.push(newTask)
        this.newTaskTitle = ""
      },
      doneTask(id) {
        let task = this.tasks.filter(task=> task.id == id)[0];
        task.done = !task.done
      },
      deleteTask(id) {
        this.tasks = this.tasks.filter(task => task.id !== id);
      }
    }
  }
</script>
