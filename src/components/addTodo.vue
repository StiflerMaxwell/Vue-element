<template>
  <div>
      <h3> Add todo</h3>

      <div class="add">
          <form @submit="onSubmit"  >
              <el-input v-model="title" ref="title" clearable type="text" placeholder="Add todos..."></el-input>

            
             <el-button type="primary" native-type="submit"  round>Submit</el-button>
          </form>
      </div>
  </div>
</template>

<script>
import {mapActions} from 'vuex'


export default {

name:'AddTodo',
data(){
    return{
        title: ''
    }
},
methods:{
    ...mapActions(['addTodo']),
    async onSubmit(e) {
        e.preventDefault();
        
       await  this.addTodo(this.title)
          this.$notify({
        title: '成功',
        message: `提交成功内容为 ${this.title}`,
        type: 'success'
      });
      this.title = ''
    }
}
}
</script>

<style scoped>
form {
  display: flex;
}
 
</style>