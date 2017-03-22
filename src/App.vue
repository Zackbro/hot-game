<template>
    <div class="facegame">
    <Hello></Hello>
    </div>
</template>

<script>
  import Hello from './components/Hello'

  export default {
    name: 'app',
    components: {
      Hello
    }
  }
</script>

<style>
  body {
    margin: 0;
  }
  .facegame {
    width: 100%;
    height: 100%;
    background-image: url(./assets/img-bg/upload_ie4dky3dheydeyrrgyzdambqgiyde_640x1059.jpg);
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
    overflow: hidden;
  }

</style>
