<script setup>
import { ref } from 'vue';
import PeopleGallery from './components/PeopleGallery.vue';
import PersonForm from './components/PersonForm.vue';
const people = ref([
  { id: 1, name: 'Alice', likes: 0, dislikes: 0 },
  { id: 2, name: 'Beiba', likes: 0, dislikes: 0 },
  { id: 3, name: 'Zhasik', likes: 0, dislikes: 0 },
  { id: 4, name: 'Alina', likes: 0, dislikes: 0 },
]);
let nextId = people.value.length + 1; 
const handleVote = (personId, type) => {
  const person = people.value.find(p => p.id === personId);
  if (person) {
    if (type === 'like') {
      person.likes++; 
    } else if (type === 'dislike') {
      person.dislikes++;
    }
  }
};
const addNewPerson = (name) => {
  if (name.trim()) {
    const newPerson = {
      id: nextId++,
      name: name,
      likes: 0,
      dislikes: 0,
    };
    people.value.push(newPerson);
  }
};
const resetVotes = () => {
  people.value.forEach(person => {
    person.likes = 0;
    person.dislikes = 0;
  });
};
</script>

<template>
  <div id="app">
    <div class="controls">
      <button @click="resetVotes" class="reset-btn">
        Reset
      </button>
      <PersonForm @add-person="addNewPerson" />
    </div>
    <PeopleGallery
      :people="people"
      @like="handleVote($event, 'like')"
      @dislike="handleVote($event, 'dislike')"
    />
  </div>
</template>

<style scoped>
#app {
  text-align: center;
  color: black;
  margin-top: 60px;
  background: white;
}

</style>