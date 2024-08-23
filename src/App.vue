<script setup>
</script>

<template>
  <header>
    <div class="container border-rounded">
      <h1 class="text-center text-light my-5">Trips Diary</h1>
      <div class="calendar bg-light p-3 m-auto rounded-4">
        <header>
          <h3></h3>
          <nav>
            <button id="previous" class="btn btn-primary fs-5 text-black m-2 "><</button>
            <button id="next" class="btn btn-primary fs-5 text-black m-2">></button>
          </nav>
        </header>
        <section class="bg-light">
          <ul class="days fs-5 d-flex justify-content-between text-align-center list-unstyled">
            <li class="p-3">Sunday</li>
            <li class="p-3">Monday</li>
            <li class="p-3">Tuesday</li>
            <li class="p-3">Wednesday</li>
            <li class="p-3">Thursday</li>
            <li class="p-3">Friday</li>
            <li class="p-3">Saturday</li>
          </ul>
          <ul class="dates"></ul>
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

</script>

<style scoped>
.calendar ul li{
  width: calc(100% / 7);
  
}

#previous:hover, #next:hover{
  background-color: white;
} 

</style>