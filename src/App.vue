<template>
  <div id="app">
 
    <div>
      
      <div class="container"> 
        <AddTodo />
        <FilterTodo />
        <Todos />
      </div>
     
    </div>
  </div>
</template>

<script>

import AddTodo from './components/addTodo'
import Todos from './components/Todos'
import FilterTodo from './components/filterTodo'
//import   './styles/app.scss'

export default {
components:{
Todos,
AddTodo,FilterTodo,
  },

 
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