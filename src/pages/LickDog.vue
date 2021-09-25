<template>
  <header>
    <img src="../assets/images/logo.gif" alt="logo">
    <h1>舔狗日记</h1>
    <p>我们是狗，舔狗</p>
  </header>
  <section :class="randClass">
    <article>
      {{ letterInfo }}
    </article>
    <address v-html="weatherInfo"></address>
  </section>
  <footer>
    <button title="点击刷新，再来一篇" @click="getRandomLetter"></button>
  </footer>
</template>

<script>
import axios from 'axios'

export default {
  name: 'lickDog',
  data() {
    return {
      randClass: 'border-1',
      weatherInfo: "",
      letterInfo: "昨天你领完红包就把我删了，我陷入久久地沉思。我想这其中一定有什么含义，原来你是在欲擒故纵，嫌我不够爱你。" +
          "无理取闹的你变得更加可爱了，我会坚守我对你的爱的。你放心好啦！今天发工资了，发了1850，给你微信转了520，支付宝1314，" +
          "还剩下16。给你发了很多消息你没回。剩下16块我在小卖部买了你爱吃的老坛酸菜牛肉面，给你寄过去了。希望你保护好食欲，" +
          "我去上班了爱你~~"
    }
  },
  created() {
    // `this` 指向 vm 实例
    this.renderWeather()
  },
  methods: {
    //随机内容
    getRandomLetter() {
      axios
          .get('https://api.oick.cn/dog/api.php')
          .then(response => {
            this.letterInfo = response.data;
          })
          .catch(error => {
            console.log(error)
          })
      this.randomNumBoth(1, 6)
      this.renderWeather()
    },
    randomNumBoth(min, max) {
      let range = max - min;
      let rand = Math.random();
      let num = min + Math.round(rand * range);
      this.randClass = 'border-' + num
    },
    renderWeather() {
      var weatherKeys = ['fbb7fed63979495f88fc1ddc7296f497', 'f3488e987bce466d8ae6b523becf278f', '95cf38cd40b84df9beae340c610e8550', '3cad9669ecba42c39ebfd73cdb566329', '6ec2f3eef9bc448ba8a72e815dd86f12'];
      var date = new Date();

      var weatherData = {};
      axios
          .get('https://free-api.heweather.net/s6/weather/now?location=auto_ip&key=' + weatherKeys[0])
          .then(response => {
            weatherData = response.data.HeWeather6[0];
            var year = date.getFullYear().toString();
            var month = (date.getMonth() + 1).toString();
            var day = date.getDate().toString();
            let city = weatherData.basic.parent_city || '';
            let cloud = weatherData.now.fl || ''
            let cond = weatherData.now.cond_txt || ''
            var weatherHTML = '<time>' + year + '-' + month + '-' + day + '</time><span>' + city + '·' + cond + '·' + cloud + '&#8451;</span>'
            this.weatherInfo = weatherHTML
          })
          .catch(error => {
            console.log(error)
          })
    }
  }

}
</script>

<style>
@font-face {
  font-family: 'MFShangYa';
  src: url('../assets/font/MFShangYa.ttf') format('truetype');
  font-weight: normal;
  font-style: normal;
}

@font-face {
  font-family: 'HYTiaoTiao';
  src: url('../assets/font/HYTiaoTiao.ttf?20200415') format('truetype');
  font-weight: normal;
  font-style: normal;
}

.border-1 {
  border-bottom-left-radius: 15px 255px;
  border-bottom-right-radius: 225px 15px;
  border-top-left-radius: 255px 15px;
  border-top-right-radius: 15px 225px
}

.border-2 {
  border-bottom-left-radius: 185px 25px;
  border-bottom-right-radius: 20px 205px;
  border-top-left-radius: 125px 25px;
  border-top-right-radius: 10px 205px
}

.border-3 {
  border-bottom-left-radius: 225px 15px;
  border-bottom-right-radius: 15px 255px;
  border-top-left-radius: 15px 225px;
  border-top-right-radius: 255px 15px
}

.border-4 {
  border-bottom-left-radius: 25px 115px;
  border-bottom-right-radius: 155px 25px;
  border-top-left-radius: 15px 225px;
  border-top-right-radius: 25px 150px
}

.border-5 {
  border-bottom-left-radius: 20px 115px;
  border-bottom-right-radius: 115px 20px;
  border-top-left-radius: 250px 15px;
  border-top-right-radius: 25px 80px
}

.border-6 {
  border-bottom-left-radius: 15px 225px;
  border-bottom-right-radius: 20px 205px;
  border-top-left-radius: 28px 125px;
  border-top-right-radius: 100px 30px
}

html,
body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
  color: #333;
}

html {
  font-size: 13.3333vw;
}

body {
  display: flex;
  flex-direction: column;
  font-family: -apple-system, 'Helvetica Neue', 'Helvetica', 'Tahoma', 'Arial', 'PingFang SC', STHeiTi, 'Microsoft Yahei';
  font-size: 16px;
  background-color: #f4f5fd;
  color: #03081a;
}

mark {
  background-color: transparent;
  background-image: -webkit-linear-gradient(#ffe21d, #ffe21d);
  background-image: -o-linear-gradient(#ffe21d, #ffe21d);
  background-image: linear-gradient(#ffe21d, #ffe21d);
  background-position: 0 85%;
  background-size: 100% 20%;
  background-repeat: no-repeat;
}

header {
  display: flex;
  align-items: center;
  padding: .2rem .4rem;
  margin: 0 0 .45rem;
  flex-shrink: 0;
  background-color: #fff;
  box-shadow: 0 0 10px rgba(0, 0, 0, .1);
}

header img {
  width: .72rem;
  height: .72rem;
}

header h1 {
  margin: .1rem 0 0;
  font-size: .64rem;
  line-height: 105%;
  font-family: "MFShangYa";
  font-weight: normal;
}

header p {
  font-size: .32rem;
  margin: .08rem 0 0 auto;
  font-family: "HYTiaoTiao"
}

section {
  font-family: "HYTiaoTiao";
  margin: auto .4rem;
  border-width: 2px 5px 4px 3px;
  border-style: solid;
  border-color: #03081a;
  overflow-y: scroll;
  display: flex;
  flex-direction: column;
  background-color: #fff;
  -webkit-overflow-scrolling: touch;
  -ms-overflow-style: none;
}

article img {
  display: none;
}

article {
  font-size: .45rem;
  margin: 0;
  padding: .4rem;
  letter-spacing: 2px;
  text-align: justify;
  flex: 1;
  overflow-y: scroll;
  -webkit-overflow-scrolling: touch;
  -ms-overflow-style: none;
}

section::-webkit-scrollbar,
article::-webkit-scrollbar {
  display: none;
}

address {
  display: flex;
  align-items: center;
  flex-shrink: 0;
  height: .8rem;
  margin: 0 .4rem;
  font-style: normal;
  color: #8c8c8c;
  font-size: .32rem;
}

address time {
  margin-right: auto;
}

footer {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-shrink: 0;
  padding: 0 0 .5rem;
  /*padding-bottom: calc(constant(safe-area-inset-bottom) + .5rem);*/
  /*padding-bottom: calc(env(safe-area-inset-bottom) + .5rem);*/
  margin: .45rem 0 0;
}

button {
  border: 0 none;
  margin: 0 .3rem;
  padding: 0;
  background-color: #fff;
  width: 1rem;
  height: 1rem;
  color: transparent;
  border-radius: 100%;
  background-image: url(../assets/images/refresh.gif);
  background-size: cover;
  background-position: 50% 50%;
  background-repeat: no-repeat;
  box-shadow: 0 0 0.2rem rgba(0, 0, 0, .2);
  cursor: pointer;
  outline: 0;
}

footer a,
footer a:active,
footer a:visited {
  vertical-align: middle;
  text-decoration: none;
  font-size: .32rem;
  color: #3078e6;
  padding: .2rem;
}

footer a:hover {
  color: #03081a;
}

tips {
  display: none;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  background-color: rgba(0, 0, 0, .5);
  border-radius: .04rem;
  font-size: .32rem;
  padding: .12rem .24rem;
  color: #fff;
}

@media (min-width: 1080px) {
  html {
    font-size: 100px;
  }

  section {
    margin: auto;
    max-width: 80%;
    border: 0 none;
    background-color: transparent;
    /*border-radius: none;*/
  }

  article {
    padding: 0 .4rem;
  }

  address {
    justify-content: flex-end;
  }

  address time {
    margin-right: .15rem;
  }
}

@media (orientation: landscape) and (min-width: 1080px) {
  header {
    padding: 10px 20px;
  }

  header img {
    width: 36px;
    height: 36px;
  }

  header h1 {
    font-size: 32px;
    margin-top: 5px;
  }

  header p {
    font-size: 18px;
    margin: 0 0 0 auto;
  }
}
</style>
