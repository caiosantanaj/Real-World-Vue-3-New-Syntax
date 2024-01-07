<script setup>
import { ref, onMounted } from 'vue'
import EventService from '../services/EventService'

const props = defineProps({
  id: {
    required: true,
  },
})

const event = ref(null)

onMounted(async () => {
  // fetch event by id and set local data
  try {
    const { data } = await EventService.getEvent(props.id)
    event.value = data
  } catch (error) {
    console.log(error)
  }
})
</script>

<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <p>{{ event.time }} on {{ event.date }} @ {{ event.location }}</p>
    <p>{{ event.description }}</p>
  </div>
  <div v-else>Loading...</div>
</template>
