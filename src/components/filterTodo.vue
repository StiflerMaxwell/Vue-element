<template>
  <div> 
      Filter todos : 
      <el-select @change="filterTodos($event)" v-model="value"  placeholder="请选择">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
  </div>
</template>

<script>

import {mapActions} from 'vuex'



export default {



name : "FilterTodo",

methods: {
...mapActions(['filterTodos'])
},
data() {
      return {
        options: [
            {
          value: '200',
          label: '200'
        },{
          value: '100',
          label: '100'
        }, {
          value: '50',
          label: '50'
        }, {
          value: '20',
          label: '20'
        }, {
          value: '10',
          label: '10'
        }],
        value: ''
      }
    }
}



</script>

<style>

</style>