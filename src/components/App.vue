<template>
    <div>
        <div v-for="week in weeks">
            week
            <div v-for="day in week">{{ day }}</div>
        </div>
    </div>
</template>

<script>
  export default {
    name: "app",
    data () {
      return {
        month: 11,
        year: 2018
      }
    },
    computed: {
      days () {

        // generation all days
        let days = [];
        let currentDay = this.$moment(`${this.year}-${this.month}-1`, 'YYYY-M-D');
        do {
          days.push(currentDay);
          currentDay = this.$moment(currentDay).add(1, 'day');
        } while (currentDay.month() + 1 === this.month);

        // add prev days
        currentDay = this.$moment(days[0]);

        const SUNDAY = 0;
        const MONDAY = 1;

        while (currentDay.day() !== MONDAY) {
          currentDay = this.$moment(currentDay).subtract(1, 'days');
          days.unshift(currentDay)
        }

        // add next days
        currentDay = this.$moment(days[days.length - 1]);
        while (currentDay.day() !== SUNDAY) {
          currentDay = this.$moment(currentDay).add(1, 'days');
          days.push(currentDay)
        }

        return days;
      },
      weeks () {
        let weeks = [];
        let week = [];

        for (let day of this.days) {
          week.push(day)
          if (week.length === 7) {
            weeks.push(week);
            week = [];
          }
        }
        return weeks
      }
    },
    created() {
      console.log(this.$moment)
    }
  }
</script>

<style scoped>

</style>