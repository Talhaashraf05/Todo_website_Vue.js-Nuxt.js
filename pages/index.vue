<template>
  <div>

          <v-text-field
          v-model="newTaskTitle"
          @click:append="addTask"
          @keyup.enter="addTask"
          class="pa-4"
            solo
            label="Enter Task"
            append-icon="mdi-plus"
            hide-details 
            clearable
          ></v-text-field>
    
          <v-list flat >
     <div v-for= '(task,i) in tasks' :key="i" :task="task"> 
      <v-list-item @click= "donetask(task)"  :class="{ 'blue lighten-5' : task.done}">
        <template v-slot:default>
          <v-list-item-action>
            <v-checkbox :input-value="task.done"></v-checkbox>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title
              :class="{'text-decoration-line-through' : task.done}"
            >
              {{task.title}}
            </v-list-item-title>
          </v-list-item-content>
          <v-list-item-action>
          <v-btn 
          @click.stop = "deletetask(task)"
          icon>
            <v-icon color="black">mdi-delete</v-icon>
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
    name: 'home',
    data (){
      return {
        newTaskTitle: '', 
      }
    },
    computed:{
      tasks(){
        console.log('hello');
        return this.$store.state.tasks
      }
    },
    methods: {
      addTask(){
        if(this.newTaskTitle)
        {
          this.$store.commit('ADD_TASK', this.newTaskTitle)
          console.log(this.$store.state.tasks);
        }
        this.newTaskTitle = '';
        },
      donetask(task){
        // let task =  this.tasks.filter(t=>t.id=== id)[0]
        // console.log(task);
        this.$store.commit('TOGGLE_TASK', task)
        console.log(task);
        // task.done = !task.done
      },
      deletetask(task){
        // this.tasks = this.tasks.filter(t => t.id !== id)
        this.$store.commit('REMOVE_TASK', task)
      },
    }
  }
</script>

<style >

</style>