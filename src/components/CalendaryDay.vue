<template>
    <div :class="classObject" @click="captureClick">
        {{ day.format('D') }}
        <ul class="event-list">
            <li v-for="event in events">{{ event.description }}</li>
        </ul>
    </div>
</template>

<script>
  export default {
    name: "calendary-day",
    props: [ 'day' ],
    computed: {
      classObject() {
        return {
          day: true,
          today: this.day.isSame(this.$moment(), 'day'),
          past: this.day.diff(this.$moment(), 'day') < 0
        }
      },
      events () {
        let mockData = [
          { description: 'Random event 1', date: this.$moment() },
          { description: 'Random event 2', date: this.$moment() }
        ]
        return mockData.filter(event => event.date.isSame(this.day,'day'))
      }
    },
    methods: {
      captureClick (event) {
        this.$store.commit('eventFormPos', { x: event.clientX, y: event.clientY });
        this.$store.commit('eventFormActive', true)
      }
    }
  }
</script>

<style scoped>

</style>