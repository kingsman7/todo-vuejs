<template lang="pug">
  #app
    .columns
      .column
      .column
        h1 Tareas y horas
        br
        input.input.is-8(type="text" v-model="title" name="title" placeholder="title" )
        input.input.is-8(type="text" v-model="time" name="time" placeholder="time" ) 
        input.button.link(type="submit" name="submit" @click="addTask(title,time)")
        p(v-if="totalTime!==0") {{totalTime}}
        div(v-for="(task,i) in tasks")
          ul
            li {{task.title}} - {{task.time}}   
            button.delete.is-medium(@click="removeTask(i)")
            br
      .column
</template>

<script>
export default {
  name: 'app',
  
  data () {
    return {
      title:'',
      time:0,
      tasks:[]
    }
  },

  computed:{
    totalTime () {
      let total = 0
      this.tasks.map(function(sum){
        total += sum.time
      })
      return total
    }
  },
  created(){
    this.tasks = JSON.parse(localStorage.getItem('tasks')) || []
  },
  methods:{
    addTask (title, time) {
      if(title, time){
        const newTask ={
          title,
          time : parseInt(time)        
        }
        this.tasks.push(newTask);
      }else(
        alert('debe llenar todos los campos')
      )
      localStorage.setItem('tasks',JSON.stringify(this.tasks))
      this.cancel ()
    },
    cancel () {
      this.title = '',
      this.time = ''
    },
    removeTask (i) {
      let remove = this.tasks.splice(i,1);
      localStorage.setItem('tasks',JSON.stringify(this.tasks))
      return remove
    } 
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
<style lang="scss">
  @import './scss/main.scss';
</style>

