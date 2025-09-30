<script setup>
import { ref } from 'vue';

const props = defineProps({
    categories: Array,
    priorities: Array
});

const emit = defineEmits(['add-task']);
const newTaskText = ref('');
const newTaskPriority = ref('Medium');
const newTaskCategory = ref('Work');

const handleSubmit = () => {
  if (newTaskText.value.trim() === '') return;

  emit('add-task', {
    text: newTaskText.value,
    priority: newTaskPriority.value,
    category: newTaskCategory.value
  });
    newTaskText.value = '';
    newTaskPriority.value = 'Medium';
    newTaskCategory.value = 'Work';
};
</script>

<template>
    <form @submit.prevent="handleSubmit" class="task-form">
        <input
            type="text"
            v-model="newTaskText"
            placeholder="Task description..."
            required
        >
         <select v-model="newTaskCategory">
      <option disabled value="">Select Category</option>
      <option v-for="cat in categories" :key="cat" :value="cat">{{ cat }}</option>
    </select>

    <select v-model="newTaskPriority">
      <option v-for="priority in priorities" :key="priority" :value="priority">{{ priority }}</option>
    </select>

    <button type="submit">Add Task</button>
    </form>
</template>

<style scoped>
.task-form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
  align-items: center;
}

.task-form input[type="text"] {
  flex-grow: 1;
  padding: 10px;
  border: 1px solid #bdc3c7;
  border-radius: 4px;
}

.task-form select, .task-form button {
  padding: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.task-form button {
  background-color: #2ecc71;
  color: white;
  transition: background-color 0.3s;
}

.task-form button:hover {
  background-color: #27ae60;
}
</style>