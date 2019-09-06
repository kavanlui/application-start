<template>
  <div
    class="task"
    draggable
    @dragover.prevent
    @dragenter.prevent
    @dragstart="pickupTask($event, taskIndex, columnIndex)"
    @click="goToTask(task)"
    @drop.stop="moveTaskOrColumn($event, column.tasks, columnIndex, taskIndex)"
  >
    <span class="w-full flex-no-shrink font-bold">
      <input type="text" :value="task.name" />
    </span>
    <p
      v-if="task.description"
      class="w-full flex-no-shrink mt-1 text-sm"
    >
      {{ task.description }}
    </p>
  </div>
</template>

<script>

import movingTasksAndColumnsMixin from '@/mixins/movingTasksAndColumnsMixin'

export default {
  mixins: [movingTasksAndColumnsMixin],
  props: {
    task: {
      type: Object,
      required: true
    },
    taskIndex: {
      type: Number,
      required: true
    }
  },
  methods: {
    goToTask (task) {
      this.$router.push({ name: 'task', params: { id: task.id } })
    },
    pickupTask (e, taskIndex, fromColumnIndex) {
      console.log(taskIndex + ' ' + fromColumnIndex)
      e.dataTransfer.effectAllowed = 'move'
      e.dataTransfer.dropEffect = 'move'
      e.dataTransfer.setData('from-task-index', taskIndex)
      e.dataTransfer.setData('from-column-index', fromColumnIndex)
      e.dataTransfer.setData('type', 'task')
    }
  }

}
</script>

<style>

</style>
