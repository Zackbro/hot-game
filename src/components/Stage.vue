<template>
  <div class="gamescreen" id="gameScreen" :class="[isActive ? hide : show]">

    <div class="stage">
      <div class="di"><img src="../assets/img-peo/upload_ifrdazjvg42dkyrrgyzdambqmeyde_91x85.png" alt=""></div>
      <div class="ji" id="gamestageNum"><img src="../assets/img-peo/upload_ifrdqolegjstgyrrgyzdambqmeyde_91x70.png" alt=""></div>
      <div class="guan"><img src="../assets/img-peo/upload_ifrdcytfg42dkyrrgyzdambqmeyde_85x85.png" alt=""></div>
    </div>

    <div class="gamestage" id="gamestage" :class="[isActive ? hide : show]">
      <img src="../assets/img-peo/upload_ie4dgmlbhfsdcyrrgyzdambqgiyde_440x118.png" class="stage-font"/>
      <img src="../assets/img-peo/loading_ieydcyrumvrgknzumuytambqgyyde_100x100.gif" class="img-show" id="imgShow"/>
      <p class="hot"><i></i>红人：<span id="nameShow"></span></p>
      <dl class="time-section">
        <dt> <span id="seeSecondBox" ref='seeSecondBox'>5</span>s</dt>
        <dd><div class="jindu1">
          <div class="jindu2"></div>
          <div class="jindu3">
            <img src="../assets/img-peo/upload_ie4dkm3fmjqteyrrgyzdambqgiyde_524x25.png" class="jindu4 progressbar animated3"  id="seeProgress" ref="seeProgress"/>
          </div>
        </div></dd>
      </dl>
    </div>

    <div class="game" id="game" :class="[isActive ? show : hide]">
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
  </div>
</template>

<script>
  import GridEvents from '../event.js'

  let time = 5;
  let total = 5;
  let see;
  let stopTimeout = false;
  export default {
    name: 'Stage',
    data () {
      return {
        isActive: this.isShow,
        show: 'show',
        hide: 'hide'
      }
    },
    props: {
      isShow: {
        type: Boolean,
        default: true
      }
    },
    watch: {
      isShow(val) {
        this.isActive= val;
      }
    },
    mounted() {
      // this.$nextTick(() => {
      // });
      GridEvents.$on('start', () => { //Hub接收事件
          this.progressTimeOut(time, total, 'seeProgress', see, this.test)
    });
      
    },
    methods: {
      progressTimeOut: function (variant, total, progressBoxId, type, callback) {
        var that = this;
        function progress() {
            if (variant < 0 || stopTimeout) {
                clearTimeout(type);
                variant = total;
                if (!stopTimeout) {
                    if (typeof(callback) === 'function') callback();
                }
            } else {
                // console.log(that.$refs.seeSecondBox);
                // 让时间等于5s
                that.$refs.seeSecondBox.innerHTML = variant;
                if (progressBoxId == 'seeProgress') {
                    that.$refs.seeProgress.style.left = ( - (1 - variant / total) * 100) + '%';
                }
                variant--;
                type = setTimeout(progress, 1000);
            }
        }
        progress();
      },
      test: function() {
        console.log(this.$refs.seeSecondBox)
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .gamestage {
    margin-bottom: 70px;
  }
  .stage {
    text-align: center;
    width: 100%;
    margin-top: 60px;
  }
  .stage div {
    display: inline-block;
  }
  .stage img {
    width: 55px;
    height: 55px;
  }
  .stage-font {
    display: block;
    margin: 20px auto 0;
    width: 331px;
    height: 88px;
  }
  .img-show {
    display: block;
    width: 344px;
    height: 220px;
    text-align: center;
    margin: 20px auto;
    border: 2px solid #010;
    box-sizing: border-box;
    background: #fff;
  }
  .hot {
    color: #fff;
    font-weight: 800;
    vertical-align: middle;
    line-height: 1.15;
    text-align: center;
    height: 22px;
    overflow: hidden;
    white-space: nowrap;
    text-overflow: ellipsis;
  }
  .time-section {
    width: 316px;
    height: 40px;
    margin: 20px auto 0;
  }
  dt {
    float: right;
    color: #97f4fe;
    font-weight: 800;
    -webkit-text-fill-color: #97f4fe;
    -webkit-text-stroke: 2px #000;
    font-size: 25px;
    text-align: right;
  }
  dd {
    margin: 0 0;
    padding: 0 0;
  }
  .jindu1{
    height: 40px;
    position: relative;
    display: block;
    width: 224px;
    text-align: center;
    margin: 0 auto;
    background-size: contain;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    background-image: url(../assets/img-bg/upload_ie3wiojrgrqteyrrgyzdambqgayde_546x47.png);
  }
  .jindu2 {
    position: absolute;
    z-index: 20;
    top: -5px;
    left: -30px;
    width: 47px;
    height: 47px;
    background-size: contain;
    background-repeat: no-repeat;
    background-position: 50% 50%;
    background-image: url(../assets/img-bg/upload_ifrwkm3bgrqteyrrgyzdambqhayde_89x85.png);
  }
  .jindu3 {
    position: absolute;
    z-index: 14;
    top:15px;
    left: -4px;
    width: 224px;
    overflow: hidden;
    height: 12px;
  }
  .jindu4 {
    vertical-align: top;
    width: 100%;
    height: 100%;
    position: absolute;
    left: 0;
    -webkit-transition: left 1s ease;
    -moz-transition: left 1s ease;
    transition: left 1s ease;
  }


  .game {
    margin-bottom: 70px;
  }
  .font-last {
    display: block;
    margin: 20px auto 0;
    width: 214px;
    height: 28px;
  }
  ul {
    width: 348.5px;
    height: 298px;
    margin: 20px auto 0; 
    padding: 0;
  }
  li {
    list-style: none;
    float: left;
    margin-right: 5px;
  }
  li img {
    width: 106px;
    height: 140px;
    border: 2px solid #010;
  }
</style>
