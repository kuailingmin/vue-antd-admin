<template>
  <div style="display: flex">
    <task-card class="task-card" title="ToDo" group="task">
      <task-item :key="index" v-for="(item, index) in todoList" :content="item" />
    </task-card>
    <task-card class="task-card" title="In Progress" group="task">
      <task-item :key="index" v-for="(item, index) in inproList" :content="item" />
    </task-card>
    <task-card class="task-card" title="Done" group="task">
      <task-item :key="index" v-for="(item, index) in doneList" :content="item" />
    </task-card>
  </div>
</template>

<script>
import TaskCard from './TaskCard'
import TaskItem from './TaskItem'
const todoList = ['任务一', '任务二', '任务三', '任务四', '任务五', '任务六']
const inproList = ['任务七', '任务八', '任务九', '任务十', '任务十一', '任务十二']
const doneList = ['任务十三', '任务十四', '任务十五', '任务十六', '任务十七', '任务十八']
export default {
  name: 'Index',
  components: {TaskItem, TaskCard},
  data () {
    return {
      todoList,
      inproList,
      doneList
    }
  }
}
</script>

<style lang="less" scoped>
  .task-card{
    margin: 0 48px;
  }
</style>
