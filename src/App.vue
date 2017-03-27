<template>
  <div class="facegame">
    <!-- $emit -->
    <Index @change='change'></Index>
    <!-- watch -->
    <Stage :indexShow='indexShow' @maskShow='maskShow'></Stage>
    <Maskdark v-show="fail"></Maskdark>
  </div>
</template>

<script>
  import Index from './components/Index'
  import Stage from './components/Stage'
  import Maskdark from './components/Maskdark'

  export default {
    name: 'app',
    data () {
      return {
        indexShow : true,
        fail: false
      }
    },
    components: {
      Index,
      Stage,
      Maskdark
    },
    methods: {
      change: function (val) {
        this.indexShow = val;
      },
      maskShow: function (val) {
        this.fail = val;
        // console.log(this.fail);
      }
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
    background-image: url(../static/img-bg/upload_ie4dky3dheydeyrrgyzdambqgiyde_640x1059.jpg);
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
    overflow: hidden;
  }

</style>
