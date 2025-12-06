<script setup>
import { computed } from 'vue';
const props = defineProps({
  person: {
    type: Object,
  }
});
const emit = defineEmits(['like', 'dislike']);
const cardClass = computed(() => {
  return {
    'person-card': true,
    'red-card': props.person.dislikes > props.person.likes
  };
});
const emitLike = () => {
  emit('like', props.person.id);
};
const emitDislike = () => {
  emit('dislike', props.person.id);
};
</script>
<template>
  <div :class="cardClass">
    <h2>{{ person.name }}</h2>
    <p>Likes: {{ person.likes }}</p>
    <p>Dislikes: {{ person.dislikes }}</p>
    <div class="buttons">
      <button @click="emitLike" class="like-btn">Like</button>
      <button @click="emitDislike" class="dislike-btn">Dislike</button>
    </div>
  </div>
</template>
<style scoped>
.person-card {
  border: 1px solid black;
  border-radius: 8px;
  padding: 20px;
  width: 200px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  background-color: white;
}
.red-card {
  border-color: red;
  background-color: rgb(238, 148, 148);
}
.buttons {
  margin-top: 15px;
  display: flex;
  justify-content: space-around;
}
.like-btn {
  background-color: #42b983;
  color: white;
  border: none;
  padding: 8px 12px;
  border-radius: 4px;
  cursor: pointer;
}
.dislike-btn {
  background-color: #ff4d4d;
  color: white;
  border: none;
  padding: 8px 12px;
  border-radius: 4px;
  cursor: pointer;
}
</style>