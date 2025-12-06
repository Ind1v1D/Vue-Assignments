<script setup>
import PersonCard from './PersonCard.vue';
defineProps({
  people: {
    type: Array,
    required: true,
  }
});
const emit = defineEmits(['like', 'dislike']);
const handleVote = (personId, type) => 
{
  emit(type, personId);
};
</script>

<template>
  <div class="gallery">
    <PersonCard
      v-for="person in people"
      :key="person.id"
      :person="person"
      @like="handleVote($event, 'like')"
      @dislike="handleVote($event, 'dislike')"  
    />
  </div>
</template>
<style scoped>
.gallery {
  justify-content: center;
  gap: 20px;
  margin-top: 20px;
  display: flex;
  flex-wrap: wrap;
}
</style>