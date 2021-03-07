<template>
  <div class="events">
    <h1>Events for Good</h1>
    <!-- add key so vue can keep track of each event
    we bind key attribute to event id.
    , event prop to add event object. that we are iterating over.
    that because the event card exports a prop, the event object.-->
    <EventCard v-for="event in events" :key="event.id" :event="event"/>
  </div>
</template>

<script>
// @ is an alias to /src
import EventCard from "@/components/EventCard.vue";
import EventService from '@/services/EventService'

export default {
  name: "EventList",
  components: {
    EventCard
  },
  data() {
    return {
      events: null
    }
  }, 
  created() {
    EventService.getEvents()
    .then( response => {
      this.events = response.data
    })
    .catch(error => {
      console.log(error)
    })
  }
};
</script>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>