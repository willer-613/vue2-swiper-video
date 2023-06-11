<template>
  <div id="app">
    <Swiper />
  </div>
</template>

<script>
// import Swiper from "./components/Swiper";
import Swiper from "./components/SiperVideo";
import b1 from "./assets/b1.jpg";
import b2 from "./assets/b2.jpg";
import b3 from "./assets/b3.jpg";
import b4 from "./assets/b4.jpg";
import b5 from "./assets/b5.jpg";
import b6 from "./assets/b6.jpg";
import s1 from "./assets/s1.jpg";
import s2 from "./assets/s2.jpg";
import s3 from "./assets/s3.jpg";
import s4 from "./assets/s4.jpg";
import s5 from "./assets/s5.jpg";
import s6 from "./assets/s6.jpg";
import leftB from "./assets/index_tab_l.png";
import rightB from "./assets/index_tab_r.png";
import leftS from "./assets/feel3.png";
import rightS from "./assets/feel4.png";
export default {
  name: "App",
  components: {
    Swiper,
  },
  data() {
    return {
      leftIcoB: leftB,
      rightIcoB: rightB,
      leftIcoS: leftS,
      rightIcoS: rightS,
      pics: [],
    };
  },
  created() {
    // setTimeout(() => {
    //   [
    //     {
    //       big: b1,
    //       small: s1,
    //     },
    //     {
    //       big: b2,
    //       small: s2,
    //     },
    //     {
    //       big: b3,
    //       small: s3,
    //     },
    //     {
    //       big: b4,
    //       small: s4,
    //     },
    //     {
    //       big: b5,
    //       small: s5,
    //     },
    //     {
    //       big: b6,
    //       small: s6,
    //     },
    //   ].forEach((item) => {
    //     this.pics.push(item);
    //   });
    // }, 5000);
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
