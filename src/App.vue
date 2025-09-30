<script setup>
import { ref, computed } from 'vue';
import TaskForm from './components/TaskForm.vue';
import TaskList from './components/TaskList.vue';

const tasks = ref([
  { id: 1, text: 'Initialize Vue Project', priority: 'High', category: 'Work', completed: true },
  { id: 2, text: 'Design basic UI layout', priority: 'Medium', category: 'Personal', completed: false },
  { id: 3, text: 'Implement task filtering', priority: 'High', category: 'Work', completed: false }
]);

const categories = ['Work', 'Personal', 'Study', 'Health'];
const priorities = ['High', 'Medium', 'Low'];

const filterCategory = ref('All');
const filterIncompleteOnly = ref(false);

const incompleteTaskCount = computed(() => {
  return tasks.value.filter(task => !task.completed).length;
});

const filteredTasks = computed(() => {
  let list = tasks.value;

  if (filterCategory.value !== 'All') {
    list = list.filter(task => task.category === filterCategory.value);
  }

  if (filterIncompleteOnly.value) {
    list = list.filter(task => !task.completed);
  }

  return list;
});

const addTask = (newTaskData) => {
  const newTask = {
    id: Date.now(),
    text: newTaskData.text.trim(),
    priority: newTaskData.priority,
    category: newTaskData.category,
    completed: false
  };
  tasks.value.push(newTask);
};

const deleteTask = (taskId) => {
  tasks.value = tasks.value.filter(task => task.id !== taskId);
};

const toggleCompletion = (taskId) => {
  const task = tasks.value.find(t => t.id === taskId);
  if (task) {
    task.completed = !task.completed;
  }
};
</script>

<template>
  <div class="container">
    <h1>📝 Vue Task Manager</h1>

    <p class="summary">
      Total Incomplete Tasks: **{{ incompleteTaskCount }}**
    </p>

    <section class="form-section">
      <h2>Add New Task</h2>
      <TaskForm 
        :categories="categories" 
        :priorities="priorities"
        @add-task="addTask"
      />
    </section>

    <hr>

    <section class="filter-section">
      <h2>Filters</h2>
      <div class="filter-controls">
        <label>Category:</label>
        <select v-model="filterCategory">
          <option value="All">All Categories</option>
          <option v-for="cat in categories" :key="cat + '_filter'" :value="cat">{{ cat }}</option>
        </select>

        <label>
          <input type="checkbox" v-model="filterIncompleteOnly">
          Show Incomplete Only
        </label>
      </div>
    </section>
      <hr>

    <section class="task-list-section">
      <h2>Task List</h2>
      <TaskList 
        :tasks="filteredTasks"
        @delete-task="deleteTask"
        @toggle-completion="toggleCompletion"
      />
    </section>
  </div>
</template>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

h1, h2 {
  color: #34495e;
}

.summary {
    font-size: 1.1em;
    padding: 10px 0;
    border-bottom: 2px solid #ecf0f1;
}

hr {
    border: 0;
    height: 1px;
    background: #ecf0f1;
    margin: 20px 0;
}

.filter-controls {
  display: flex;
  gap: 20px;
  align-items: center;
  margin-bottom: 20px;
}

.filter-controls select {
  padding: 8px;
  border: 1px solid #bdc3c7;
  border-radius: 4px;
}
</style>
