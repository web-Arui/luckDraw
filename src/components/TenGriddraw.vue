<template>
  <div>
    <div class="indexback">
      <div
        :class="['dianquan', 'tl' + (index + 1)]"
        v-for="(item, index) in 18"
        :key="item"
      ></div>
      <img class="index2" src="../assets/image/index2.gif" />
      <img class="index3" src="../assets/image/index3.png" />
      <div class="boxfu">
        <div class="box">
          <div :class="['list',cjChange == index+1 ? 'listac' : '']" v-for="(item, index) in 10" :key="index">
            <img class="hezhi" src="../assets/image/hezhi.png" />
          </div>
        </div>
        <div @click="lottery" class="chou">
          <img class="chouimg" src="../assets/image/chou2.png" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cjIn:false,//判断是否在抽奖中
      cjChange:0, //抽奖过程KEY
      showAgain: false, //是否抽奖后显示再抽一次按钮
      timer:null,//定时器
      prizeResult:null,//比对的
    };
  },
  methods: {
    lottery() {
      if (this.cjIn) {
        return;
      } else {
        this.cjIn = true;
      }
      clearInterval(this.timer);
      this.timer = setInterval(this.changePrize, 80);
      let res = {
        prizeResult: Math.floor(Math.random() * 10 + 1),
      };
        setTimeout(() => {
          clearInterval(this.timer)
          this.timer = setInterval(this.changePrize,160)
          setTimeout(() => {
            clearInterval(this.timer)
            this.timer=setInterval(this.changePrize,300)
            setTimeout(() => {
              this.prizeResult = res.prizeResult
            }, 1000);
          }, 1000);
        }, 2000);
    },
    //抽奖过程奖品切换
    changePrize() {
      let cjChange = this.cjChange
     cjChange++;
      cjChange = cjChange > 10 ? 1 : cjChange;
      this.cjChange = cjChange
      if (this.prizeResult == this.cjChange) {
        clearInterval(this.timer);
          this.showAgain= true,
        setTimeout(() => {
         console.log('中奖',this.cjChange)
         alert('中奖'+this.cjChange)
         this.cjChange=0
         this.cjIn=false
         this.prizeResult = null
        }, 500);
      }
    },
  },
};
</script>

<style scoped>
.indexback {
  width: 100%;
  position: relative;
}
.index2 {
  width: 716px;
  height: 374px;
  position: absolute;
  top: 200px;
  left: 17px;
  z-index: 2;
}
.index3 {
  position: absolute;
  top: 311px;
  left: 89px;
  width: 578px;
  height: 462px;
}
.boxfu {
  position: absolute;
  top: 344px;
  left: 121px;
  width: 520px;
  height: 390px;
  z-index: 3;
}
.box {
  position: relative;
  width: 100%;
  height: 100%;
}
.list {
  width: 123px;
  height: 123px;
  position: absolute;
  display: flex;
  justify-content: center;
  align-items: center;
  background: url("data:image/png;base64,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")
    no-repeat;
  background-size: 100% 100%;
}
.box .list:nth-child(1) {
  top: 0;
  left: 0;
}
.box .list:nth-child(2) {
  top: 0;
  left: 130px;
}
.box .list:nth-child(3) {
  top: 0;
  left: 260px;
}
.box .list:nth-child(4) {
  top: 0;
  left: 390px;
}
.box .list:nth-child(5) {
  top: 130px;
  left: 390px;
}
.box .list:nth-child(6) {
  top: 260px;
  left: 390px;
}
.box .list:nth-child(7) {
  top: 260px;
  left: 260px;
}
.box .list:nth-child(8) {
  top: 260px;
  left: 130px;
}
.box .list:nth-child(9) {
  top: 260px;
  left: 0px;
}
.box .list:nth-child(10) {
  top: 130px;
  left: 0px;
}
.chou {
  position: absolute;
  top: 130px;
  left: 130px;
  width: 256px;
  height: 129px;
  /* animation: glow 800ms ease-out infinite alternate;
  box-shadow: 0 0 20px rgba(0, 255, 0, 0.6); */
}
@keyframes glow {
  0% {
    border-color: #393;
    box-shadow: 0 0 5px rgba(0, 255, 0, 0.2), inset 0 0 5px rgba(0, 255, 0, 0.1),
      0 1px 0 #393;
  }
  100% {
    border-color: #6f6;
    box-shadow: 0 0 20px rgba(0, 255, 0, 0.6) inset 0 0 10px
      rgba(0, 255, 0, 0.4) 0 1px 0 #6f6f;
  }
}
.chouimg {
  width: 100%;
  height: 100%;
}
.listac {
  width: 153px;
  height: 153px;
  transform: translate(-17px, -15px);
  background: url(../assets/image/listac.png) no-repeat;
  background-size: 100% 100%;
}
.hezhi {
  width: 115px;
  height: 116px;
  position: relative;
}
.num {
  position: absolute;
  top: 50px;
  left: 0;
  width: 100%;
  text-align: center;
  font-size: 42px;
  font-family: Adobe Heiti Std;
  font-weight: normal;
  color: #f2e657;
  text-shadow: 0px 4px 4px rgba(203, 28, 22, 0.45);
}
.num2 {
  width: 50px;
  font-size: 25px;
  top: 48px;
  left: 30px;
  line-height: 26px;
}
.num3 {
  font-size: 14px;
}

.rgba {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  z-index: 10;
}
.rgbabox {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 11;
}
.rgbox {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.rgbaback {
  width: 707px;
  height: 667px;
  position: relative;
}
.rgtips {
  position: absolute;
  top: 320px;
  left: 0;
  width: 100%;
  text-align: center;
  font-size: 37px;
  font-family: PingFang SC;
  font-weight: bold;
  color: #ffffff;
}
.jitext {
  width: 479px;
  height: 88px;
  background: #f9cb42;
  border: 2px solid #f07933;
  box-shadow: 0px 2px 8px 0px rgba(115, 8, 21, 0.5);
  border-radius: 44px;
  text-align: center;
  line-height: 88px;
  font-size: 32px;
  font-family: PingFang SC;
  font-weight: 500;
  color: #bd1122;
  margin-top: 26px;
}
.quanclose {
  width: 71px;
  height: 71px;
  margin-top: 37px;
}
.thankyou {
  width: 170px;
  height: 49px;
  position: absolute;
  top: 500px;
  left: 270px;
}
.smalltips {
  font-size: 32px;
  font-family: PingFang SC;
  font-weight: 500;
  color: #ffe6bb;
  position: absolute;
  top: 610px;
  left: 0;
  width: 100%;
  text-align: center;
}
.hezhiz {
  position: absolute;
  width: 116px;
  height: 118px;
  top: 437px;
  left: 300px;
}
.zhongtext {
  position: absolute;
  top: 488px;
  left: 0;
  width: 100%;
  text-align: center;
  font-size: 42px;
  font-family: Adobe Heiti Std;
  font-weight: normal;
  color: #f2e657;
  text-shadow: 0px 4px 4px rgba(203, 28, 22, 0.45);
}
.zhongtext2 {
  font-size: 14px;
}
.chouci {
  text-align: center;
  position: absolute;
  top: 1362px;
  left: 0;
  width: 100%;
  color: white;
  font-size: 28px;
  font-family: PingFang SC;
}

/* 烟花 */
.text {
  position: absolute;
  top: 0;
  z-index: 5;
  width: 100%;
  height: 100%;
  color: #e49bd4;
  word-wrap: break-word;
}
p {
  font-weight: 400;
  font-size: 1em;
}
h1 {
  width: 100%;
  height: 100%;
  line-height: 350px;
  font-size: 6em;
  font-weight: 900;
  position: relative;
  margin: 0;
}

/* FOR HOVER
---------------------------------------*/
.front,
.back {
  background: #3f2860;
  width: 100%;
  height: 100%;
  display: block;
  top: 0;
  left: 0;
  position: absolute;
  backface-visibility: hidden;
  overflow: hidden;
}
.back {
  z-index: 10;
  transform: rotateY(180deg);
}
/*
#container:hover #card{
  transform: rotateY(-180deg);
}
*/
.back p {
  line-height: normal;
  position: relative;
  margin: 0 5%;
  top: 50%;
  transform: translateY(-50%);
}

@media only screen and (max-width: 600px) {
  h1 {
    line-height: 175px;
  }
  #card {
    width: 300px;
    height: 400px;
  }
}
.firework-grp {
  display: block;
  /* width: 100%;
  height: 100%;
  position: absolute; */
  color: white;
  color: #535396;
}
.firework-grp2 {
  transform: rotate(180deg);
  color: #2c1c44;
  z-index: 6;
}
.firework-grp3 {
  transform: rotate(-75deg);
  color: #e339bd;
  z-index: 7;
}
.firework {
  font-size: 10px;
  display: block;
  width: 100px;
  height: 100px;
  position: absolute;
  color: #2fc7cd;
}
.firework2 {
  color: #fa913e;
}
.firework3 {
  color: #a92160;
}
.firework4 {
  color: #e3a8c8;
}
.firework5 {
  color: #d3d7e0;
}
.firework6 {
  color: #aa89f0;
}
.firework7 {
  color: #e8b69e;
}

/* SIZES
------------------------------------*/
.size01 {
  transform: scale(0.1);
}
.size02 {
  transform: scale(0.2);
}
.size03 {
  transform: scale(0.4);
}
.size04 {
  transform: scale(0.4);
}
.size05 {
  transform: scale(0.5);
}
.size08 {
  transform: scale(0.8);
}

/* POSITION
------------------------------------*/
.pos1 {
  left: 30px;
  top: 216px;
}
.pos12 {
  left: 27px;
  top: 213px;
}
.pos2 {
  left: 65px;
  top: 65px;
}
.pos5 {
  left: 62px;
  top: 62px;
}
.pos6 {
  left: 60px;
  top: 60px;
}
.pos3 {
  left: 226px;
  top: 65px;
}
.pos32 {
  left: 223px;
  top: 63px;
}
.pos33 {
  left: 222px;
  top: 62px;
}
.pos4 {
  left: 554px;
  top: 216px;
}
.pos42 {
  left: 551px;
  top: 213px;
}

.pos7 {
  left: 5%;
  top: -5%;
}
.pos8 {
  left: 75%;
  top: 20%;
}

/* FIREWORK
------------------------------------*/
.drops-grp {
  display: block;
  width: 8.5em;
  height: 8.5em;
  position: absolute;
}
.drops-grp2 {
  display: block;
  width: 8.5em;
  height: 8.5em;
  position: absolute;
  transform: rotate(45deg);
}
.drop {
  display: block;
  width: 1em;
  height: 2em;
  overflow: hidden;
  position: absolute;
  opacity: 0;
}
.drop:before {
  content: "";
  display: block;
  width: 1em;
  height: 1em;
  background: currentColor;
  border-radius: 50%;
}
.drop:after {
  content: "";
  display: block;
  position: relative;
  top: -0.4em;
  width: 0;
  height: 0;
  border-top: 1.4em solid currentColor;
  border-left: 0.5em solid transparent;
  border-right: 0.5em solid transparent;
}
.drop-1 {
  left: 3.75em;
  top: 0;
  animation: drop1anim 1s ease-in-out infinite;
  /* opacity: 1; */
}
.drop-2 {
  top: 3.25em;
  right: 0;
  animation: drop2anim 1s ease-in-out infinite;
  /* opacity: 1; */
}
.drop-3 {
  left: 3.75em;
  bottom: 0;
  animation: drop3anim 1s ease-in-out infinite;
  /* opacity: 1; */
}
.drop-4 {
  top: 3.25em;
  left: 0;
  animation: drop4anim 1s ease-in-out infinite;
  /* opacity: 1; */
}
.firework-2 .drop-1 {
  animation-delay: 0.5s;
}
.firework-2 .drop-2 {
  animation-delay: 0.5s;
}
.firework-2 .drop-3 {
  animation-delay: 0.5s;
}
.firework-2 .drop-4 {
  animation-delay: 0.5s;
}

/* FIREWORK DELAY
------------------------------------*/
.delay1 .drop-1 {
  animation-delay: 0.25s;
}
.delay1 .drop-2 {
  animation-delay: 0.25s;
}
.delay1 .drop-3 {
  animation-delay: 0.25s;
}
.delay1 .drop-4 {
  animation-delay: 0.25s;
}

.delay2 .drop-1 {
  animation-delay: 0.75s;
}
.delay2 .drop-2 {
  animation-delay: 0.75s;
}
.delay2 .drop-3 {
  animation-delay: 0.75s;
}
.delay2 .drop-4 {
  animation-delay: 0.75s;
}

/* keyframes
------------------------------------*/
@keyframes drop1anim {
  0% {
    top: 3.25em;
    opacity: 0;
    transform: scale(0.3);
  }
  25% {
    opacity: 0;
  }
  50% {
    opacity: 1;
    transform: scale(1);
  }
  100% {
    top: -0.75em;
    opacity: 0;
    transform: scale(0.3);
  }
}
@keyframes drop2anim {
  0% {
    right: 3.75em;
    opacity: 0;
    transform: scale(0.3) rotate(90deg);
  }
  25% {
    opacity: 0;
  }
  50% {
    opacity: 1;
    transform: scale(1) rotate(90deg);
  }
  100% {
    right: -0.25em;
    opacity: 0;
    transform: scale(0.3) rotate(90deg);
  }
}
@keyframes drop3anim {
  0% {
    bottom: 3.25em;
    opacity: 0;
    transform: scale(0.3) rotate(180deg);
  }
  25% {
    opacity: 0;
  }
  50% {
    opacity: 1;
    transform: scale(1) rotate(180deg);
  }
  100% {
    bottom: -0.75em;
    opacity: 0;
    transform: scale(0.3) rotate(180deg);
  }
}
@keyframes drop4anim {
  0% {
    left: 3.75em;
    opacity: 0;
    transform: scale(0.3) rotate(-90deg);
  }
  25% {
    opacity: 0;
  }
  50% {
    opacity: 1;
    transform: scale(1) rotate(-90deg);
  }
  100% {
    left: -0.25em;
    opacity: 0;
    transform: scale(0.3) rotate(-90deg);
  }
}
.yanhuaa {
  position: absolute;
  top: 605px;
  left: 260px;
  width: 100px;
  height: 100px;
  animation: anan 1.2s ease infinite;
  z-index: 2;
}
.yanhuaa2 {
  width: 70px;
  height: 70px;
  left: 423px;
  top: 650px;
  animation-delay: 0.3s;
}
.gif {
  position: absolute;
  top: -45px;
  left: 52px;
  width: 100%;
}
@keyframes anan {
  0% {
    opacity: 0;
    transform: scale(0.1);
  }
  25% {
    opacity: 0;
  }
  50% {
    opacity: 1;
    transform: scale(100%);
  }
  60% {
    opacity: 0.89;
    transform: scale(100%);
  }
  100% {
    opacity: 0;
    transform: scale(100%);
  }
  100% {
    transform: scale(100%);
  }
}

.dianquan {
  position: absolute;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  animation: sandong 1s linear infinite;
  z-index: 4;
}

.tl1 {
  top: 483px;
  left: 261px;
}
.tl2 {
  top: 480px;
  left: 293px;
  animation-delay: 0.3s;
}
.tl3 {
  top: 480px;
  left: 332px;
  animation-delay: 0s;
}
.tl4 {
  top: 480px;
  left: 370px;
  animation-delay: 0.1s;
}
.tl5 {
  top: 480px;
  left: 408px;
  animation-delay: 0.7s;
}
.tl6 {
  top: 480px;
  left: 446px;
  animation-delay: 0.2s;
}
.tl7 {
  top: 483px;
  left: 478px;
  animation-delay: 0.6s;
}
.tl8 {
  top: 513px;
  left: 478px;
  animation-delay: 0.2s;
}
.tl9 {
  top: 545px;
  left: 478px;
  animation-delay: 0.1s;
}
.tl10 {
  top: 575px;
  left: 478px;
  animation-delay: 0.7s;
}
.tl11 {
  top: 578px;
  left: 446px;
  animation-delay: 0.6s;
}
.tl12 {
  top: 578px;
  left: 408px;
  animation-delay: 0.4s;
}
.tl13 {
  top: 578px;
  left: 370px;
  animation-delay: 0.1s;
}
.tl14 {
  top: 578px;
  left: 330px;
  animation-delay: 0.3s;
}
.tl15 {
  top: 578px;
  left: 292px;
  animation-delay: 0s;
}
.tl16 {
  top: 575px;
  left: 261px;
  animation-delay: 0.4s;
}
.tl17 {
  top: 545px;
  left: 261px;
  animation-delay: 0.3s;
}
.tl18 {
  top: 512px;
  left: 261px;
  animation-delay: 0.1s;
}

@keyframes sandong {
  0% {
    background: radial-gradient(
      circle,
      #ffffff 2%,
      #ffffff 2%,
      #fffc433e 6%,
      #e75959 30%,
      #df7b7b 60%
    );
    /* box-shadow: 0px 3px 7px 0px rgba(11, 156, 63, 0.53), -1px -2px 10px 0px rgba(0, 0, 0, 0.4); */
  }
  20% {
    background: #fd945a;
    background-image: radial-gradient(5px 5px, circle cover, yellow, orange);

    box-shadow: 0px 3px 10px 0px rgba(155, 55, 15, 0.35),
      -1px -2px 10px 0px rgba(0, 0, 0, 0.4);
  }
  40% {
    background: #ef78f0;
    box-shadow: 0px 3px 7px 0px rgba(141, 17, 141, 0.35),
      -1px -2px 10px 0px rgba(0, 0, 0, 0.4);
  }
  60% {
    background: red;
    box-shadow: 0px 3px 7px 0px rgba(215, 51, 108, 0.35),
      -1px -2px 8px 0px rgba(0, 0, 0, 0.16);
  }
  80% {
    background: #ee5b99;
    box-shadow: 0px 3px 7px 0px rgba(215, 51, 108, 0.35),
      -1px -2px 8px 0px rgba(0, 0, 0, 0.16);
  }
  100% {
    background: #86a2ea;
    box-shadow: 0px 3px 7px 0px rgba(69, 4, 75, 0.35),
      -1px -2px 8px 0px rgba(0, 0, 0, 0.16);
  }
}
.dong1 {
  position: absolute;
  top: 1440px;
  left: 27px;
  width: 140px;
  height: 72px;
  animation: lryi 2s linear infinite;
}
.dong2 {
  position: absolute;
  top: 1666px;
  right: 25px;
  width: 98px;
  height: 112px;
  animation: suo 1.5s linear infinite;
}
.dong3 {
  position: absolute;
  top: 1712px;
  right: 25px;
  width: 141px;
  height: 71px;
  animation: lryi 2s linear infinite;
  animation-delay: 1.5s;
}
.dong4 {
  position: absolute;
  top: 3730px;
  left: 0px;
  width: 100px;
  height: 104px;
  animation: suo 1s linear infinite;
}
.dong5 {
  position: absolute;
  top: 3766px;
  left: -24px;
  width: 161px;
  height: 60px;
  animation: lryi 2s linear infinite;
  animation-delay: 1s;
}
.dong6 {
  position: absolute;
  top: 3188px;
  right: 25px;
  width: 98px;
  height: 112px;
  animation: suo 1.5s linear infinite;
}
.dong7 {
  position: absolute;
  top: 3236px;
  right: 25px;
  width: 141px;
  height: 71px;
  animation: lryi 2s linear infinite;
  animation-delay: 1.2s;
}
.gifhong {
  width: 460px;
  height: 163px;
  position: absolute;
  top: 380px;
  left: 136px;
}
@keyframes lryi {
  0% {
    transform: translateX(-30px);
  }
  50% {
    transform: translateX(30px);
  }
  100% {
    transform: translateX(-30px);
  }
}
@keyframes suo {
  0% {
    transform: scale(0.8);
  }
  50% {
    transform: scale(1);
  }
  100% {
    transform: scale(0.8);
  }
}
</style>