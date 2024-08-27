<template>
  <div class="modal">
      <div class="modal-inner bg-dark rounded-5 m-5 opacity-75 text-light">
        <form>
          <div class="form-row">
            <div class="form-group">
              <label for="inputEmail4">Destination Locality</label>
              <input type="email" class="form-control" id="inputEmail4" placeholder="Email">
            </div>
          </div>
          <div class="form-group">
            <label for="inputAddress">Address</label>
            <input type="text" class="form-control" id="inputAddress" placeholder="1234 Main St">
          </div>
          <div class="form-group">
            <label for="inputAddress">Dettagli Viaggio:</label>
            <input type="text" class="form-control" id="inputAddress" placeholder="1234 Main St">
          </div>
          <div class="form-group">
            <div class="form-check my-3">
              <input class="form-check-input" type="checkbox" id="gridCheck">
              <label class="form-check-label text-danger" for="gridCheck">
                Check me out
              </label>
            </div>
          </div>
          <button type="submit" class="btn btn-primary my-2">Sign in</button>
        </form>
      <button class="modal-close btn btn-primary my-2">Close Modal</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'ModalComponent',
  setup () {
    

    return {

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

.modal-inner{
  background-color: blue;
  padding: 100px;
}


</style>