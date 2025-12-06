<script setup>
import { ref } from 'vue';
const emit = defineEmits(['add-person']);
const newPersonName = ref('');
const submitForm = () => {
  if (newPersonName.value.trim() !== '') {
    emit('add-person', newPersonName.value);
    newPersonName.value = ''; 
  }
};
</script>
<template>
  <form @submit.prevent="submitForm" class="person-form">
    <input
      type="text"
      v-model="newPersonName"
      placeholder="Enter new person's name"
      required
    />
    <button type="submit">Add Person</button>
  </form>
</template>
<style scoped>
.person-form {
  display: flex;
  gap: 10px;
  align-items: center;
}
.person-form input {
  padding: 8px;
  border: 1px solid gray;
  border-radius: 4px;
  flex: 1;
}
.person-form button {
  padding: 8px 16px;
  border: none;
  background-color: #42b983;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}
</style>