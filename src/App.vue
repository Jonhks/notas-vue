<template lang='pug'>
#app
  link(href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet")
  .container
    .row
      h2 Administrador de tareas
      span.col.m4 {{ name }} 
      span.col.m4.offset-m3 Tiempo Total estimado :{{ totalTime }}
    .row
      p Nueva tarea
      input.col.m5(type="text" placeholder="Tarea" 
      v-model="newTask.title")
      input.col.m5.offset-m1(type="number" placeholder="Horas estimadads"
      v-model="newTask.time")
    .row
      a.button.waves-effect.waves-light.btn(@click="addTask") Guardar
      a.button.waves-effect.waves-light.btn.offset(@click="cancel") Cancelar 
    .row  
      div
        h3 Mi lista de tareas
        p(style="color: tomato", v-show="!tasks.length") Aun no hay tareas cargadas
      div(v-show="tasks.length")
        ol
          li(v-for="(task,index) in tasks")
            p Mi tarea: {{ task.title }}, estimo {{ task.time }} horas
            span(@click="removeTask(index)")
              i.material-icons delete
              hr
       
          


</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      name: 'Jonathan Parra',
      tasks: [],
      newTask:{
        title: '',
        time: undefined
      }
    }
  },
  created () {
    this.tasks = JSON.parse(localStorage.getItem('task')) || []
  }, computed: {
    totalTime () {
       if (!this.tasks.length) { 
         return 0 
       }
       let total = 0
        this.tasks.forEach(t => {
         total += parseInt(t.time)
      })
      return total
    }
  },
  methods: {
    addTask () {
      if (!this.newTask.title || !this.newTask.time) { 
        return 
      }
      this.tasks.push({
        title: this.newTask.title,
        time: this.newTask.time
      })
      localStorage.setItem("tasks", JSON.stringify(this.tasks))
      this.newTask.title = ''
      this.newTask.time = 0
    },
    removeTask (index) {
      this.tasks.splice(index, 1)
      localStorage.setItem("tasks", JSON.stringify(this.tasks))
    },
        cancel () {
      this.newTask.title = ''
      this.newTask.time = 0
    }
  }
}
</script>

<style lang="scss">
@import './sass/main.scss';
.offset{
  margin-left: 5%;
}

</style>
