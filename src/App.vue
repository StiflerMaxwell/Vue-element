<template>
  <div id="app">
 
    <div>
      
      <div class="container"> 

        <AddTodo />
        <FilterTodo />
      <Todos   />
      </div>
     
    </div>
  </div>
</template>

<script>

import AddTodo from './components/addTodo'
import Todos from './components/Todos'
 import FilterTodo from './components/filterTodo'
 

export default {
components:{
Todos,
AddTodo,FilterTodo
  },

  methods: {
    startHacking () {
      this.$notify({
        title: 'It works!',
        type: 'success',
        message: 'We\'ve laid the ground work for you. It\'s time for you to build something epic!',
        duration: 5000
      })
    }
  }
}
</script>

<style>
#app {
  
  text-align: center;
font-family: "Helvetica Neue",Helvetica,"PingFang SC","Hiragino Sans GB","Microsoft YaHei","微软雅黑",Arial,sans-serif;
 
}
 
body{
   margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  max-width: 1100px;
  margin: auto;
  overflow: auto;
  padding: 0 2rem;
}
 
</style>