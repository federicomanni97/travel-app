<template>
  <div class="modal">
      <div class="bordermodal modal-inner bg-primary rounded-5 m-5 opacity-75 text-light">
        <form  @submit.prevent="inviaDati">
          <h1>Travel Notes:</h1>
          <div class="form-row">
            <div class="form-group my-2">
              <label for="inputEmail4">Destination Locality:</label>
              <input type="email" class="form-control" v-model="Destination" id="inputEmail4" placeholder="Your Destination">
            </div>
          </div>
          <div class="form-group my-2">
            <label for="inputAddress">Dates:</label>
            <input type="text" class="form-control" v-model="Dates" id="inputAddress" placeholder="Dates">
          </div>
          <div class="form-group my-2">
            <label for="inputAddress">Trip Details:</label>
            <input type="text" class="form-control" v-model="TripDetails" id="inputAddress" placeholder="Trip Details">
          </div>
        </form>
      <button class="modal-close btn btn-dark m-2" @click="toggleModal()" >Close Modal</button>
      <button type="submit" class="modal-close btn btn-success m-2" @click="inviaDati()">Inserisci Dati</button>
    </div>
  </div>
</template>

<script>

import { ref } from 'vue'

export default {
  name: 'ModalComponent',
  props: ['toggleModal', 'modalTriggers', ],
  data() {
    return {
      Destination: '',
      Dates: '',
      TripDetails: '',
    }
  },
  methods: {
    // inviaForm() {
    //   console.log('Destinazione:', this.Destination),
    //   console.log('Data:', this.Dates),
    //   console.log('Dettagli Viaggio:', this.TripDetails)

    // },

    inviaDati() {
      this.$emit('invia-dati', this.Destination, this.Dates, this.TripDetails),
      this.toggleModal();
    }
  }
}
</script>
<style scoped>

.modal{
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  width: 100%;
  z-index: 99;
  display: flex;
  align-items: center;
  justify-content: center;
}

.bordermodal{
  border: 1px solid white;
}

.modal-inner{
  background-color: blue;
  padding: 100px;
}


</style>