<template>
  <div class="calendar text-light h-100">
     <div class="d-flex justify-content-end flex-column align-items-end mb-4">
         <nav>
             <button id="previous" class="btn style-button fs-3 text-black" @click="prevMonth"><</button>
             <button id="next" class="btn style-button fs-3 text-black" @click="nextMonth">></button>
         </nav>
         <h3 class="text-uppercase month fs-1 fw-bold"> {{ getMonthName(selectedMonth) }} {{ selectedMonthYear.year }}</h3>
     </div>
     <div class="days list-unstyled fs-3 text-uppercase" >
         <ul class="days" v-for="(day, index) in dayNames" :key="`day-${index}`">
             <li class="rounded-4 ">{{ day }}</li>
         </ul>
     </div>
     <ul class="dates list-unstyled rounded-10 w-100 fs-1" id="dates" >
         <li class="number square rounded-circle fs-2"
          v-for="(day, index) in getDays(selectedMonthYear.year, selectedMonthYear.month)"
         :key="`day-${index}`" 
         @click="() => toggleModal('buttonTrigger')"
         :class="{'active-day': day.number !== null}">
             {{ day.number }}
         </li>
         <div class="fs-6">
            <p class="bg-primary rounded-3 p-1">Destinazione: {{ Destination }}</p>
            <p class="bg-primary rounded-3 p-1">Data: {{ Dates }}</p>
            <p class="bg-primary rounded-3 p-1">Dettagli Viaggio: {{ TripDetails }}</p>
         </div>
     </ul>
 </div>
 <div>
     <ModalComponent v-if="modalTriggers.buttonTrigger"
     :toggleModal="() => toggleModal('buttonTrigger')"
     @invia-dati="aggiornaDati">
         <h2> My ModalComponent</h2>
     </ModalComponent>
 </div>
</template>

<script>

import { ref } from 'vue';
import ModalComponent from './ModalComponent.vue';

export default {
name: 'CalendarComponent',
props: ['Destination', 'Dates', 'TripDetails'],
components: {
 ModalComponent
},
data() {
     const modalTriggers = ref({
         buttonTrigger: false,
         timedTrigger: false
     })
     const toggleModal = (trigger) => {
     modalTriggers.value[trigger] = !modalTriggers.value[trigger];
     }
   return {
     Destination: '',
     Dates: '',
     TripDetails: '',
     ModalComponent,
     modalTriggers,
     toggleModal,
     showModal: false,
     downloading: false,
     selectedMonth: null,
     selectedYear: null,
     showMonthSelection: false,
     dayNames: [
       'Saturday',
       'Sunday',
       'Monday',
       'Tuesday',
       'Wednesday',
       'Thursday',
       'Friday'
     ],
     monthNames: [
       { month: 1, title: 'January' },
       { month: 2, title: 'February' },
       { month: 3, title: 'March' },
       { month: 4, title: 'April' },
       { month: 5, title: 'May' },
       { month: 6, title: 'June' },
       { month: 7, title: 'July' },
       { month: 8, title: 'August' },
       { month: 9, title: 'September' },
       { month: 10, title: 'October' },
       { month: 11, title: 'November' },
       { month: 12, title: 'December' }
     ]
   }
 },
 components: {
   ModalComponent
 },
 computed: {
   startOfMonthDay() {
     const date = this.selectedMonthYear
     const firstDay = new Date(date.year, date.month - 1, 1) // gets first day of the selected month
     return firstDay.getUTCDay()
   },
   currentMonthYear() {
     const date = new Date()
     const month = date.getMonth() + 1
     const Year = date.getFullYear()
     return { month: month, year: Year }
   },
   selectedMonthYear() {
     const date = new Date()
     let month
     let year
     if (this.selectedMonth != null) {
       month = this.selectedMonth
     }
     else {
       month = date.getMonth() + 1
     }
     if (this.selectedYear != null) {
       year = this.selectedYear
     }
     else {
       year = date.getFullYear()
       this.selectedYear = year  
     }
     return { month: month, year: year }
   }
 },
 created() {
   if (this.selectedMonth === null) {
     this.selectedMonth = this.selectedMonthYear.month
   }
 },
 methods: {
   aggiornaDati(destination, dates, tripDetails) {
     this.Destination = destination
     this.Dates = dates
     this.TripDetails = tripDetails
   },
   updateSelectedYear(year) {
     // this.selectedYear = year
   },
   updateSelectedMonth(month) {
     this.selectedMonth = month
     this.showMonthSelection = false
   },
   doSomething() {
     alert('Doing something')
   },
   getMonthName(month) {
     return this.monthNames.find(item => item.month === month).title
   },
   getCashupReports() {
     this.$store.dispatch('getCashUpRecords')
   },
   getDays(year, month) {
     const date = new Date(year, month - 1, 1)
     const result = []
     let dayOffset = 2 + this.startOfMonthDay
     if (dayOffset === 7) {
       dayOffset = 7 - dayOffset
     }
     let i
     for (i = 0; i < dayOffset; i++) {
       result.push({ number: null, date: null, fullDate: null })
     }

     while (date.getMonth() === month - 1) {
       const dd = String(date.getDate()).padStart(2, '0')
       const mm = String(date.getMonth() + 1).padStart(2, '0')
       const yyyy = date.getFullYear()
       const shortDate = `${yyyy},${mm},${dd}`
       const item = { number: date.getDate(), date: shortDate, fullDate: date.toString() }
       result.push(item)
       date.setDate(date.getDate() + 1)
     }
     return result
   }, 
   prevMonth() {
     if (this.selectedMonth === 1) {
       this.selectedMonth = 12
       this.selectedYear = this.selectedYear - 1
     }
     else {
       this.selectedMonth = this.selectedMonth - 1
     }
   },
   nextMonth() {
     if (this.selectedMonth === 12) {
       this.selectedMonth = 1
       this.selectedYear = this.selectedYear + 1
     }
     else {
       this.selectedMonth = this.selectedMonth + 1
     }
   },
   toggleModal(trigger) {
     this.modalTriggers[trigger] = !this.modalTriggers[trigger];
   },    
 }
}
</script>
<style scoped>

.dates li.active-day:hover{
background-color: lightblue;
cursor: pointer;
}

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

.number{
height: 50px;
width: 50px;
display: grid;
place-items: center;

}

.month{
color: lightblue;
}

.square li{
 height: 80px;
 width: 80px;
 display: grid;
 place-items: center;
}

.style-button{
 background-color: transparent;
 border: 0px;
}

</style>