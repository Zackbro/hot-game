<template>
  <div class="game" id="game">
    <img src="../assets/img-peo/upload_ie3tayjthbsdcyrrgyzdambqgayde_394x52.png" class="font-last"/>
    <ul class="avatar-list" id="avatarList">
      <li onclick="compare(this)"><img src="../assets/img-peo/upload_ie4gezrygjrdcmrrgyzdambqgiyde_218x286.jpg" alt=""></li>
      <li onclick="compare(this)"><img src="../assets/img-peo/upload_ie4gezrygjrdcmrrgyzdambqgiyde_218x286.jpg" alt=""></li>
      <li onclick="compare(this)"><img src="../assets/img-peo/upload_ie4gezrygjrdcmrrgyzdambqgiyde_218x286.jpg" alt=""></li>
      <li onclick="compare(this)"><img src="../assets/img-peo/upload_ie4gezrygjrdcmrrgyzdambqgiyde_218x286.jpg" alt=""></li>
      <li onclick="compare(this)"><img src="../assets/img-peo/upload_ie4gezrygjrdcmrrgyzdambqgiyde_218x286.jpg" alt=""></li>
      <li onclick="compare(this)"><img src="../assets/img-peo/upload_ie4gezrygjrdcmrrgyzdambqgiyde_218x286.jpg" alt=""></li>
    </ul>
    <p class="hot">谁是<i></i>红人：<span id="hotname"></span></p>
    <dl class="time-section">
      <dt> <span id="timeSecondBox">10</span>s</dt>
      <dd><div class="jindu1">
        <div class="jindu2"></div>
        <div class="jindu3">
          <img src="../assets/img-peo/upload_ie4dkm3fmjqteyrrgyzdambqgiyde_524x25.png" class="jindu4" id="timeProgress"/>
        </div>
      </div></dd>
    </dl>
  </div>
</template>

<script>
  export default {
    name: 'hello',
    data () {
      return {
        imgList: []
      }
    },
    methods: {
      progressTimeOut: function () {
        console.log('progressTimeOut');
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
