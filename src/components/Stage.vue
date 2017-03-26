<template>
  <div class="gamescreen" v-show="!screenShow">
    <div class="stage">
      <div class="di"><img :src=imgUrl.di alt=""></div>
      <div class="ji"><img :src=stageArray[stage-1] alt=""></div>
      <div class="guan"><img :src=imgUrl.guan alt=""></div>
    </div>
    <div class="gamestage" v-show="!stageShow">
      <img :src=imgUrl.stage class="stage-font"/>
      <img :src=chooseGirl.group class="img-show"/>
      <p class="hot"><i></i>红人：{{chooseGirl.name}}<span id="nameShow"></span></p>
      <dl class="time-section">
        <dt> <span ref='seeSecondBox'>{{stageTime}}</span>s</dt>
        <dd><div class="jindu1">
          <div class="jindu2"></div>
          <div class="jindu3">
            <img :src=imgUrl.second class="jindu4 progressbar animated3" ref="seeProgress"/>
          </div>
        </div></dd>
      </dl>
    </div>
    <div class="game" v-show="gameShow">
    <img :src=imgUrl.gameFont class="font-last"/>
      <ul class="avatar-list">
        <li @click="compare(item)" v-for="item in listChange"><img :src=item alt=""><div class="wrong" style="display: none"></div></li>
      </ul>
      <p class="hot">谁是<i></i>红人：{{chooseGirl.name}}<span></span></p>
      <dl class="time-section">
        <dt> <span ref='timeSecondBox'>{{gameTime}}</span>s</dt>
        <dd><div class="jindu1">
          <div class="jindu2"></div>
          <div class="jindu3">
            <img :src=imgUrl.second class="jindu4" ref="timeProgress"/>
          </div>
        </div></dd>
      </dl>
    </div>
  </div>
</template>

<script>
  import GridEvents from '../event.js'
  import img from '../img.js'
  import {stageArray, bisai, fontArray} from '../constant.js'

  let see;
  let timeLeft;
  let stopTimeout = false;
  let guan, easy, normal, hard, showGirl
  // chooseGirl.list[0] 是正确答案
  export default {
    name: 'Stage',
    data () {
      return {
        imgUrl: img,
        stageTime : 5,
        totalStage: 5,
        gameTime : 10,
        totalGame: 10,
        screenShow: this.indexShow,
        stageShow: this.indexShow,
        gameShow: false,
        chooseGirl: {},
        listChange: [],
        nameChange: '',
        stage: 1,
        stageArray: stageArray,
        maskShow : false,
        winTimeout: false
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
        this.screenShow= val;
        this.stageShow= val;
      },
      maskShow(val) {
       this.$emit('maskShow', val);
     }
   },
   mounted() {
      GridEvents.$on('start', () => { //GridEvent接收事件
        this.play();
      });
      GridEvents.$on('replay', () => { //GridEvent接收事件
        this.maskShow = false;
        this.stageShow = false;
        this.gameShow = false;
        this.replay();          
      });     
    },
    methods: {
      // 进度条
      progressTimeOut: function (variant, total, progressBoxId, time, type, callback) {
        var that = this;
        function progress() {
          if (variant < 0 || stopTimeout) {
            clearTimeout(type);
            variant = total;
            if (that.winTimeout) {
              that.stage++;
              that.nextStage();
              that.winTimeout = false;
              that.stopTimeout = true;
              return;
            }
            if (!stopTimeout) {
              if (typeof(callback) === 'function') callback();
            }
          } else {
                // 让时间等于5
                that.$refs[time].innerHTML = variant;
                that.$refs[progressBoxId].style.left = ( - (1 - variant / total) * 100) + '%';
                variant--;
                type = setTimeout(progress, 1000);
              }
            }
            progress();
          },
          showGame: function() {
            this.stageShow = true;
            this.gameShow = true;
            let temp = this.chooseGirl.list;
            this.listChange = this.randomOrder(temp);
            this.progressTimeOut(this.gameTime, this.totalGame, 'timeProgress', 'timeSecondBox', timeLeft, this.fail)
          },
      // easy 随机排序， 
      randomOrder: function(targetArray) {
        var arrayLength = targetArray.length;
        var tempArray1 = [];
        for (var i = 0; i < arrayLength; i++) {
          tempArray1[i] = i
        }
        // 将每一项的选项打乱
        var tempArray2 = [];
        for (var i = 0; i < arrayLength; i++) {
          tempArray2[i] = tempArray1.splice(Math.floor(Math.random() * tempArray1.length), 1)
        }
        var tempArray3 = [];
        for (var i = 0; i < arrayLength; i++) {
          tempArray3[i] = targetArray[tempArray2[i]]
        }
        return tempArray3
      },
      compare: function (src) {
        if (src.indexOf(this.chooseGirl.list[0]) > -1) {
          console.log('you win');
          this.gameTime = 10;
          stopTimeout = true;
          this.winTimeout = true;

        } else {
          this.gameTime = 10;
          stopTimeout = true;
          this.fail();
          return false;
        }
      },
      // 显示stage
      nextStage: function () {
        this.gameShow = false;
        this.stageShow = false;
        this.play(this.stage);
      },
      play: function (guan) {
        guan = guan || 1;
        if (guan == 1) {
          easy = this.randomOrder(bisai.easy);
          normal = this.randomOrder(bisai.normal);
          hard = this.randomOrder(bisai.hard);
        }
        if (guan >= 1 && guan <= 7) {
          showGirl = easy[guan - 1];
        } else if (guan > 7 && guan <= 15) {
          showGirl = normal[guan - 8];
        } else {
          showGirl = hard[guan - 16];
        }
        this.chooseGirl = showGirl;
        // 倒计时
        stopTimeout = false;
        this.progressTimeOut(this.stageTime, this.totalStage, 'seeProgress', 'seeSecondBox', see, this.showGame)
      },
      fail: function () {
        this.maskNumber();
        this.maskShow = true;
      },
      replay: function() {
        stopTimeout = false;
        this.progressTimeOut(this.stageTime, this.totalStage, 'seeProgress', 'seeSecondBox', see, this.showGame)
      },
      maskNumber: function () {
       GridEvents.$emit('maskNumber', this.stage, this.chooseGirl.list[0]);
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
    background-image: url(../../static/img-bg/upload_ie3wiojrgrqteyrrgyzdambqgayde_546x47.png);
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
    background-image: url(../../static/img-bg/upload_ifrwkm3bgrqteyrrgyzdambqhayde_89x85.png);
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
  .wrong {
    position: absolute;
    top: 0;
    left: 15px;
    width: 82px;
    height: 136px;
    background-position: center center;
    background-size: contain;
    background-image: url(../../static/img-bg/upload_ie3tem3gha2teyrrgyzdambqgayde_135x135.png);
    background-repeat: no-repeat;
  }
  ul {
    width: 348.5px;
    height: 298px;
    margin: 20px auto 0; 
    padding: 0;
  }
  li {
    position: relative;
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
