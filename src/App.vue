<template>
    <div class="facegame">
      <!-- $emit -->
      <Index @change='change'></Index>
      <!-- watch -->
      <Stage :indexShow='indexShow'></Stage>
    </div>
</template>

<script>
  import Index from './components/Index'
  import Stage from './components/Stage'

  export default {
    name: 'app',
    data () {
      return {
        indexShow : true
      }
    },
    components: {
      Index,
      Stage
    },
    methods: {
      change: function (val) {
        this.indexShow = val;
      }
    }
  }
</script>

<style>
  body {
    margin: 0;
  }
  .show {
    display: block;
  }
  .hide {
    display: none;
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
