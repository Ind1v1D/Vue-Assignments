<script setup>
import TaskItem from './TaskItem.vue';

const props = defineProps({
  tasks: Array
});

const emit = defineEmits(['delete-task', 'toggle-completion']);

const handleDeletion = (taskId) => {
  emit('delete-task', taskId);
};

const handleToggle = (taskId) => {
  emit('toggle-completion', taskId);
};
</script>

<template>
  <p v-if="tasks.length === 0" class="no-tasks">
    No tasks match your current filter criteria.
  </p>

  <ul v-else class="task-list">
    <TaskItem
      v-for="task in tasks"
      :key="task.id"
      :task="task"
      @delete-task="handleDeletion"
      @toggle-completion="handleToggle"
    />
  </ul>
</template>

<style scoped>
.task-list {
  list-style: none;
  padding: 0;
}

.no-tasks {
    text-align: center;
    padding: 20px;
    border: 1px dashed #bdc3c7;
    border-radius: 6px;
    color: #7f8c8d;
}
</style>