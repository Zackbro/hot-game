<template>
  <div>
    <div class="share-bg"></div>
    <div class="sicong1" id="sicong1" style="display:none">
      <img src="">
    </div>
    <div class="sicong2" id="sicong2" style="display:none">
      <img src="">
    </div>
    <div class="share-download" id="shareAll" style="display:none"></div>
    <div class="share-box">
      <div class="share-text" id="shareText">{{font}}</div>
      <ul class="share-list">
        <li id="bufu" @click="replay"><div class="share-btn share-bufu"></div></li>
        <li id="xuanyao">
          <div class="share-btn who"></div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import GridEvents from '../event.js'
import {stageArray, bisai, fontArray} from '../constant.js'

export default {
  data() {
    return {
      font: fontArray
    }
  },
  methods: {
    replay: function () {
      GridEvents.$emit('replay');
    }
  },
  mounted() {
      GridEvents.$on('maskNumber', (stage) => { //GridEvent接收事件
       console.log(stage);
       if (stage >= 1 && stage <= 10) {
            console.log(fontArray);
            this.font = fontArray.easy[Math.floor(Math.random() * 3)].replace('X', stage);
        } else if (stage >= 11 && stage <= 22) {
            this.font = fontArray.normal[Math.floor(Math.random() * 3)].replace('X', stage);
        } else {
            this.font = fontArray.hard[0];
        }
      });     
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .share-bg {
    position: absolute;
    right: 0;
    z-index: 100;
    top: 0;
    bottom: 0;
    background: rgba(0,0,0,0.7);
    width: 100%;
  }
  .share-box {
    position: absolute;
    left: 0;
    letter-spacing: 4px;
    z-index: 173;
    top: 35%;
    width: 100%;
  }
  .share-text {
    line-height: 1.5;
    color: #fff;
    font-size: 1.75em;
    width: 94%;
    text-align: center;
    letter-spacing: 0;
    margin: 0 auto 50px;
  }
  .share-list li {
    text-align: center;
  }
  .share-btn {
    cursor: pointer;
    display: inline-block;
    width: 187px;
    height: 72px;
    background-size: contain;
    background-repeat: no-repeat;
  }
  .share-bufu {
    background-image: url(../../static/img-bg/upload_ifrwgyzrgu4deyrrgyzdambqhayde_356x143.png)
  }
  .who {
    background-image: url(../../static/img-bg/upload_ie3wmnbshbrteyrrgyzdambqgayde_356x143.png);
  }
  ul li {
    margin: 0;
    padding: 0;
  }
  li {
    list-style-type: none;
  }
</style>
