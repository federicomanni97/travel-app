<script setup>
</script>

<template>
  <header>
    <div class="container border-rounded">
      <h1 class="text-center text-light my-5 text-uppercase">Trips Diary</h1>
      <div class="calendar my-5 py-5 bg-light p-3 m-auto rounded-4">
        <header>
          <div class="d-flex justify-content-end flex-column align-items-end mb-4">
            <nav>
              <button id="previous" class="btn btn-light fs-3 text-black" @click="prevMonth"><</button>
              <button id="next" class="btn btn-light fs-3 text-black" @click="nextMonth">></button>
            </nav>
            <h3 class="text-uppercase month fs-1 fw-bold"> {{ monthName }} {{ year }}</h3>
          </div>
        </header>
        <section class="">
          <ul class="days list-unstyled fs-3 text-uppercase">
            <li class="">Sunday</li>
            <li class="">Monday</li>
            <li class="">Tuesday</li>
            <li class="">Wednesday</li>
            <li class="">Thursday</li>
            <li class="">Friday</li>
            <li class="">Saturday</li>
          </ul>
          <ul class="dates list-unstyled fs-2" id="dates" ref="dates"></ul>
        </section>
      </div>
    </div>
  </header>

  <main>
    <div>
      
    </div>
  </main>
</template>

<script>
// primo
export default {
  data() {
    return {
      month: new Date().getMonth(),
      year: new Date().getFullYear(),
      monthNames: [
        'January',
        'February',
        'March',
        'April',
        'May',
        'June',
        'July',
        'August',
        'September',
        'October',
        'November',
        'December'
      ]
    };
  },

  computed: {
    monthName() {
      return this.monthNames[this.month];
    }
  },

  methods: {
    prevMonth() {
      this.month--;
      if (this.month < 0) {
        this.month = 11;
        this.year--;
      }
      this.renderCalendar();
    },

    nextMonth() {
      this.month++;
      if (this.month > 11) {
        this.month = 0;
        this.year++;
      }
      this.renderCalendar();
    },

    renderCalendar() {
      // Calculate start and end dates
      const start = new Date(this.year, this.month, 1).getDay();
      const endDate = new Date(this.year, this.month + 1, 0).getDate();
      
      // Render dates
      let datesHtml = '';
      
      for (let i = 0; i < start; i++) {
      datesHtml += `<li></li>`;
      }

      for (let i = 1; i <= endDate; i++) {
        datesHtml += `<li class="p-3">${i}</li>`;
      }

      this.$refs.dates.innerHTML = datesHtml;
    }
  },

  mounted() {
    this.renderCalendar();
  }
};

</script>

<style scoped>
.calendar ul li{
  display: grid;
  
}

.calendar-grid {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
}

.days, .dates {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  justify-items: center;
}

#previous:hover, #next:hover{
  background-color: lightblue;
} 

.days{
  color: lightblue;
}

.month{
  color: lightblue;
}

</style>