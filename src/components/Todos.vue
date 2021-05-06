<template>
  <div>

      <h3>todos</h3>
      <div class="todos">
 
  <el-table 
      v-loading="loading"
          :data="allTodos.filter(data => !search || data.title.toLowerCase().includes(search.toLowerCase()))"
          style="width: 100%">
          <el-table-column
            prop="id"
            label="id"
            width="180">
          </el-table-column>
    
 
 
    <el-table-column   prop="title" label="title">
 
      <template slot-scope="scope" >
        {{scope.row.title}}
        <i v-if="scope.row.completed" class="el-icon-circle-check green icons" ></i>
       </template>
    </el-table-column>


<el-table-column width="180" align="right">
      <template slot="header"   slot-scope="{}" >
         <el-input
          v-model="search"
           type="text"
           clearable       
          placeholder="输入关键字搜索"></el-input>
          
 
      </template>
      <template slot-scope="scope">
          <div class="icons">
          <i @click="handleUpdate(scope.row)" type="primary"   class="el-icon-edit-outline clickable"></i>
          <i @click="open(scope.row.id)" type="danger"    class="el-icon-delete danger clickable"></i>
         </div>
      </template>
    </el-table-column>
      
    </el-table>


          
      </div>


      <el-dialog title="EDIT Todo" :visible.sync="dialogFormVisible">
        <el-form :model="todo">
           <el-form-item label="ID" :label-width="formLabelWidth">
            <el-input v-model="todo.id" autocomplete="off" :disabled="true" :value= todo.id  ></el-input>
          </el-form-item>

          <el-form-item label="Title" :label-width="formLabelWidth">
            <el-input v-model="todo.title" autocomplete="off"  :value= todo.title  clearable></el-input>
          </el-form-item>
          <el-form-item label="Completed" :label-width="formLabelWidth">          
          <el-switch
            v-model="todo.completed"
            active-color="#13ce66"
            inactive-color="#ff4949"
            active-text="已完成"
            inactive-text="未完成"
             >
          </el-switch>
          </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
          <el-button @click="CancelUpdate()">取 消</el-button>
          <el-button type="primary" @click="UpdateTodo(todo)">确 定</el-button>
        </div>
      </el-dialog>
  </div>


  
</template>

<script>
 
import {mapGetters, mapActions} from 'vuex'
 //import Pagination from './components/pagination'
 
export default {
 
data(){
    return {
        
        loading:true,
         dialogFormVisible: false,
        todo: {
          
          id: this.id,
           title : this.title,
           completed : this.completed  
        },
        formLabelWidth: '80px',
         search:"",
        
    }

}

,



name: "Todos",
 
methods: {
...mapActions(['fetchTodos','deleteTodo','updateTodos']),
...mapActions({
        deleteTodo: 'deleteTodo', // 将 `this.deleteTodo()` 映射为 `this.$store.dispatch('deleteTodo')`
      }),
  
    handleUpdate(obejct){

        this.dialogFormVisible= true;
        this.todo.id = obejct.id;
        this.todo.title = obejct.title;
        this.todo.completed = obejct.completed;
 
    },

    UpdateTodo(todo){
        this.dialogFormVisible = false
        const updtodo = {
          id: todo.id,
          title: todo.title,
          completed : todo.completed,
        }

      this.updateTodos(updtodo)
      .then(() => {
           this.$message({            
            type: 'success',
            message: '修改成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消修改'
          });          
        });
     

    },

   
    CancelUpdate(){

      this.dialogFormVisible = false;
      this.$message({
            type: 'info',
            message: '已取消修改'
          });
    },
    open(id) {
        this.$confirm('此操作将永久删除该todo, 是否继续?', '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
            this.$store.dispatch('deleteTodo', id);
            this.deleteTodo(id);
        })
        .then(() => {
           this.$message({            
            type: 'success',
            message: '删除成功!'
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: '已取消删除'
          });          
        });
      }
      ,
    
 
},
  
computed: mapGetters(['allTodos']),
created(){
 
 setTimeout(() => {
   this.fetchTodos();
   this.loading = false;
 }, 1000);
    
 
},


}
</script>

<style>
 
 .icons{
   font-size: 20px;
 }
.clickable{

 color:#409EFF;
      padding: 0 10px;
    font-size: 20px;
   cursor: pointer;
}

.front{
  display: flex;
   
    align-items: center;
}

.green{
  color:#67C23A;
}
.danger{

color:#F56C6C;
}


.cell{


  display: flex;
    justify-content: space-between;
    align-items: center;

}
 
</style>