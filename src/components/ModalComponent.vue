<template>
  <div class="modal">
      <div class="modal-inner bg-dark rounded-5 m-5 opacity-75 text-light">
        <form>
          <h1>Travel Notes:</h1>
          <div class="form-row">
            <div class="form-group">
              <label for="inputEmail4">Destination Locality:</label>
              <input type="email" class="form-control" id="inputEmail4" placeholder="Your Destination">
            </div>
          </div>
          <div class="form-group">
            <label for="inputAddress">Dates:</label>
            <input type="text" class="form-control" id="inputAddress" placeholder="Dates">
          </div>
          <div class="form-group">
            <label for="inputAddress">Trip Details:</label>
            <input type="text" class="form-control" id="inputAddress" placeholder="Trip Details">
          </div>
        </form>
      <button class="modal-close btn btn-primary my-2" @click="toggleModal()" >Close Modal</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'ModalComponent',
  props: ['toggleModal', 'modalTriggers', ],
  data() {
    return {

    }
  },
  methods: {

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

.modal-inner{
  background-color: blue;
  padding: 100px;
}


</style>