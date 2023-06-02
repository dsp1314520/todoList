<script setup>
import Edit from './components/Edit.vue'
import axios from "axios";
import { onMounted, ref } from 'vue';

// TODO: 列表渲染
// 1.创建一个列表
const list = ref([])
// 创建一个函数来获取数据
const getList = async () => {
  const res = await axios.get('/list')
  // console.log(res.data);
  list.value = res.data
}
onMounted(() => getList())

// TODO: 删除功能
// 获取id 
const onDelet = async (row) => {
  console.log(row.id);
  const res = await axios.delete(`/del/${row.id}`)
  // console.log(res);
  if (!res.data) {
    return console.log('删除失败！');
  }
  getList()
}


// TODO: 编辑功能

</script>

<template>
  <div class="app">
    <el-table :data="list">
      <el-table-column label="ID" prop="id"></el-table-column>
      <el-table-column label="姓名" prop="name" width="150"></el-table-column>
      <el-table-column label="籍贯" prop="place"></el-table-column>
      <el-table-column label="操作" width="150">
        <template #default="{ row }">
          <el-button type="primary" link>编辑</el-button>
          <el-button type="danger" @click="onDelet(row)" link>删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
  <Edit />
</template>

<style scoped>
.app {
  width: 980px;
  margin: 100px auto 0;
}
</style>
