<template>
  <div>

      <h3>todos</h3>
      <div class="todos">

        <!-- <el-card class="box-card">
<div v-for="todo in allTodos" :key="todo.id" class="todo">
            {{todo.title}}

           <i @click="deleteTodo(todo.id)" class="el-icon-delete"></i>
          </div>
</el-card> -->


<el-table 
  v-loading="loading"
      :data="allTodos"
      style="width: 100%">
      <el-table-column
        prop="id"
        label="id"
        width="180">
      </el-table-column>
    
 
  <el-table-column prop="title" label="title">
      <template slot-scope="scope">
         {{scope.row.title}}
        <i @click="handleDelete(scope.row.id)" class="el-icon-delete"></i>
      </template>
    </el-table-column>

    </el-table>


          
      </div>


      
  </div>
</template>

<script>
 
import {mapGetters, mapActions} from 'vuex'
 
export default {
 
data(){
    return {
        loading:true
    }

}

,
name: "Todos",
methods: {
...mapActions(['fetchTodos','deleteTodo']),
...mapActions({
        deleteTodo: 'deleteTodo', // 将 `this.deleteTodo()` 映射为 `this.$store.dispatch('deleteTodo')`
      }),
  async handleDelete(id)
{
    this.$store.dispatch('deleteTodo', id);
     await  this.deleteTodo(id);

    this.$notify({
            title: '成功',
            message: `成功删除了 ${id}`,
            type: 'success'
          });
},

},
  
computed: mapGetters(['allTodos']),
created(){
 
 setTimeout(() => {
   this.fetchTodos();
   this.loading = false;
 }, 1000);
    
 
}
}
</script>

<style scoped>
 

i {
  position: absolute;
  bottom: 10px;
  right: 10px;
  color: black;
  cursor: pointer;
}
 
</style>