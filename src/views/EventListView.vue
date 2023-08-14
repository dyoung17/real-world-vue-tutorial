<script setup>
import EventCard from '../components/EventCard.vue'
import  { onMounted, ref } from 'vue'
import EventService from '../services/EventService.js'

const events = ref(null)

onMounted(() =>{
 EventService.getEvents()
    .then((resp) => {
      events.value = resp.data
    })
    .catch((error) => {
      console.log(error)
    })
})
</script>

<template>
  <h1>Events for Good</h1>
  <div class="events"></div>
  <EventCard v-for="event in events" :key="event.id" :event="event"></EventCard>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
