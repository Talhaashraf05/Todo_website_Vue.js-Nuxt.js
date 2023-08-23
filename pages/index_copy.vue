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
            
  
      <v-list
        flat
      >
      <div v-for= 'task in tasks' :key="task.id">
  
        <v-list-item @click= "donetask(task.id)"  :class="{ 'blue lighten-5' : task.done}">
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
            @click.stop = "deletetask(task.id)"
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
          tasks: [
            {
              id: 1,
              title: 'wake up',
              done: false
  
            },
            {
              id: 2,
              title: 'Get bannas',
              done: false
              
            },
            {
              id: 3,
              title: 'Eat bananas',
              done: false
              
            },
            {
              id: 4,
              title: 'Close fridge',
              done: false
            }
          ]
        }
      },
      methods: {
        addTask(){
          let newtask = {
            id: Date.now() ,
            title: this.newTaskTitle, 
            done: false
          }
          this.tasks.push(newtask)
          this.newTaskTitle = ''
          },
        donetask(id){
          let task =  this.tasks.filter(t=>t.id=== id)[0]
          // console.log(task);
          console.log(id);
          
          task.done = !task.done
        },
        deletetask(id){
          this.tasks = this.tasks.filter(t => t.id !== id)
        },
  
      }
    }
  </script>
  
  <style >
  
  </style>