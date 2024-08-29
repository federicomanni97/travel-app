<template>
  <div class="container h-100">
  <header class="text-center my-5">
    <h1 class="text-light">Travel Trips</h1>
  </header>
  <main>
    <div>
      <CalendarComponent/>
    </div>
  </main>
</div>
</template>

<script>

import CalendarComponent from './components/CalendarComponent.vue';

export default {
  components: {
    CalendarComponent
  },
}


</script>

<style scoped>

</style>