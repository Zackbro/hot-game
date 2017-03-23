<template>
  <div class="gamestart" id="gamestart" v-show="isActive">
    <div class="title"></div>
    <div class="sub-title she"></div>
    <div class="girls">
      <img src="../assets/img-peo/upload_ie4tqmjwmvrdcyrrgyzdambqgqyde_564x211.jpg" class="group-girls"/>
    </div>   
    <div class="sub-title animated fadeIn she-up"></div>
    <ul class="photo-list" id="photo-list">
      <li class="animated fadeIn"><img src="../assets/img-peo/upload_ie3wmmtcge2tcyrrgyzdambqgayde_181x162.jpg" alt=""></li>
      <li class="animated fadeIn"><img src="../assets/img-peo/upload_ifqtcnbtgi2tcyrrgyzdambqgyyde_181x162.jpg" alt=""></li>
      <li class="animated fadeIn"><img src="../assets/img-peo/upload_ifrdkntcgi2tcyrrgyzdambqmeyde_181x162.jpg" alt=""></li>
      <li class="animated fadeIn"><img src="../assets/img-peo/upload_ifqtsojtgm2tcyrrgyzdambqgyyde_181x162.jpg" alt=""></li>
      <li class="animated fadeIn"><img src="../assets/img-peo/upload_ie4giylcgm2tcyrrgyzdambqgiyde_181x162.jpg" alt=""></li>
      <li class="animated fadeIn"><img src="../assets/img-peo/upload_ie3tayztgq2tcyrrgyzdambqgayde_181x162.jpg" alt=""></li>
    </ul>
    <footer>
      <div id="start" class="animated fadeIn" @click="start"></div>
    </footer>
  </div>
</template>

<script>
import GridEvents from '../event.js'

  export default {
    data () {
      return {
        isActive: this.indexShow,
      }
    },
    props: {
      indexShow: {
        type: Boolean,
        default: true
      }
    },
    watch: {
      indexShow(val) {
        this.isActive= val; 
      },
      isActive(val) {
        this.$emit('change', val);
      }
    },
    methods: {
      start: function () {
        this.isActive = false;
        console.log(this.isActive);
        GridEvents.$emit('start');
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .show {
    display: block;
  }
  .hide {
    display: none;
  }
  li {
    list-style-type: none;
  }
  .title {
    position: absolute;
    z-index: 10;
    text-align: center;
    top: 0;
    left: 0;
    background-size: contain;
    background-repeat: no-repeat;
    width: 100%;
    height: 102px;
    vertical-align: middle;
    background-image: url(../assets/img-bg/upload_ie4wmmrymvsdcyrrgyzdambqgqyde_640x189.png);
    background-position: center center;
  }
  .sub-title {
    margin-top: 8px;
    width:100%;
    height: 32px;
    text-align: center;
    font-weight: 800;  
    background-position: center center;
    background-size: contain;
    background-repeat: no-repeat;  
  }
  .she {
    margin-top: 100px;
    background-image: url(../assets/img-bg/upload_ie4wkntggzsdcyrrgyzdambqgqyde_255x51.png);
  }
  .she-up {
    height: 34px;
    background-image: url(../assets/img-bg/upload_ifqtqojvmnsdcyrrgyzdambqgyyde_255x51.png);
  }
  .girls {
    text-align: center;
  }
  .group-girls {
    width: 357px;
    height: 136px;
    border: 2px solid #010;
  }
  ul {
    padding: 0 0;
    margin: 0 0;
  }
  .photo-list {
    width: 374px;
    height: 248px;
    clear: both;
    margin: 0 auto;
  }
  .photo-list li {
    float: left;
    padding-top: 10px;
    margin-left: 10px;
    width: 109px;
    height: 112px;
    opacity: 0;
  }
  .photo-list img{
    width: 109px;
    height: 112px;
    border: 2px solid #010;
  }
  footer {
   text-align: center;
 }
 #start {
  background-image: url(../assets/img-bg/upload_ie4wkytgg43teyrrgyzdamjqgqyde_366x141.png);
  width: 187px;
  height: 68px;
  background-size: contain;
  background-repeat: no-repeat;
  display: inline-block;
  cursor: pointer;
}

.animated {
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
}
.fadeIn {
  -webkit-animation-name: fadeIn;
  animation-name: fadeIn;
}

@-webkit-keyframes fadeIn {
  from {
    opacity: 0
  }

  to {
    opacity: 1
  }
}

@keyframes fadeIn {
  from {
    opacity: 0
  }

  to {
    opacity: 1
  }
}


@-webkit-keyframes progressbar {
  from {
    left: 0
  }

  to {
    left: -100%
  }
}

@keyframes progressbar {
  from {
    left: 0
  }

  to {
    left: -100%
  }
}

.progressbar {
  -webkit-animation-name: progressbar;
  animation-name: progressbar
}
</style>
