<template>
    <div>
        <div>{{ formatedDate }}</div>
        <button class="" @click="dec">-</button>
        <button class="" @click="inc">+</button>
    </div>
</template>

<script>
  export default {
    name: "current-month",
    computed: {
      month() {
        return this.$store.state.currentMonth;
      },
      year() {
        return this.$store.state.currentYear;
      },
      formatedDate() {
        return this.$moment(`${this.year}-${this.month}-1`, 'YYYY-M-D').format('MMMM YYYY');
      }
    },
    methods: {
      dec () {
        if (this.month === 1) {
          this.$store.commit('setCurrentMonth', 12);
          this.$store.commit('setCurrentYear', this.year - 1);
        } else {
          this.$store.commit('setCurrentMonth', this.month - 1);
        }
      },
      inc () {
        if (this.month === 12) {
          this.$store.commit('setCurrentMonth', 1);
          this.$store.commit('setCurrentYear', this.year + 1);
        } else {
          this.$store.commit('setCurrentMonth', this.month + 1);
        }
      }
    }
  }
</script>

<style scoped>

</style>