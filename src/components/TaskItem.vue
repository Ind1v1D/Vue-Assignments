<script setup>
const props = defineProps({
  task: Object
});

const emit = defineEmits(['delete-task', 'toggle-completion']);

const handleDelete = () => {
  emit('delete-task', props.task.id);
};

const handleToggle = () => {
  emit('toggle-completion', props.task.id);
};
</script>

<template>
  <li
    class="task-item"
    :class="{ 
      'completed': task.completed, 
      'priority-high': task.priority === 'High', 
      'priority-medium': task.priority === 'Medium',
      'priority-low': task.priority === 'Low' 
    }"
  >
    <div class="task-details">
      <span class="task-text">{{ task.text }}</span>
      <span class="task-meta">[{{ task.category }} | {{ task.priority }}]</span>
    </div>

    <div class="task-actions">
      <button @click="handleToggle">
        {{ task.completed ? 'Undo' : 'Complete' }}
      </button>
      
      <button class="delete-btn" @click="handleDelete">
        Delete
      </button>
    </div>
  </li>
</template>

<style scoped>
.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
  margin-bottom: 8px;
  border-radius: 6px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
  background-color: #ffffff;
  transition: all 0.3s;
  border-left: 5px solid #bdc3c7;
}

.task-details {
    display: flex;
    flex-direction: column;
}

.task-meta {
    font-size: 0.8em;
    color: #7f8c8d;
}

.task-actions button {
  margin-left: 10px;
  padding: 8px 12px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  background-color: #3498db;
  color: white;
}

.task-actions .delete-btn {
  background-color: #e74c3c;
}

.completed {
  background-color: #f0f3f5;
  opacity: 0.7;
  border-left-color: #27ae60;
}

.completed .task-text {
  text-decoration: line-through;
  color: #7f8c8d;
}

.priority-high { border-left-color: #e74c3c !important; }
.priority-medium { border-left-color: #f39c12 !important; }
.priority-low { border-left-color: #2ecc71 !important; }
</style>