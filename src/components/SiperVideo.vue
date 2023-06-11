<template>
  <div class="pc-slide">
    <div class="view">
      <div class="swiper-container">
        <div class="swiper-wrapper">
          <div class="swiper-slide" v-for="(item, index) in pics" :key="index">
            <VideoPlayer
              v-if="item.type === 'video'"
              :ref="`VideoPlayer${index}`"
              :videoInit="{
                poster: '//vjs.zencdn.net/v/oceans.png',
                type: 'video/mp4',
                src: item.src,
              }"
            />
            <img :src="item.src" alt v-else />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import b1 from "../assets/b1.jpg";
import b2 from "../assets/b2.jpg";
import b3 from "../assets/b3.jpg";
import b4 from "../assets/b4.jpg";
import b5 from "../assets/b5.jpg";
import b6 from "../assets/b6.jpg";
import VideoPlayer from "./VideoPlayer";

export default {
  name: "Swiper",
  components: {
    VideoPlayer,
  },
  data() {
    return {
      player: null,
      viewSwiper: null,
      pics: [
        {
          src: "//vjs.zencdn.net/v/oceans.mp4",
          type: "video",
        },
        {
          src: b1,
          type: "pic",
        },
        {
          src: b2,
          type: "pic",
        },
        {
          src: b3,
          type: "pic",
        },
        {
          src: b4,
          type: "pic",
        },
        {
          src: b5,
          type: "pic",
        },
        {
          src: b6,
          type: "pic",
        },
      ],
    };
  },
  mounted() {
    this.$nextTick(() => {
      this.init();
    });
  },
  methods: {
    init() {
      const _this = this;
      this.viewSwiper = new window.Swiper(".view .swiper-container", {
        loop: true,
        onSlideChangeEnd: function (swiper) {
          console.log(11111);
          const { activeLoopIndex } = swiper;
          if (_this.pics[activeLoopIndex].type === "video") {
            console.log(
              swiper,
              _this.$refs[`VideoPlayer${activeLoopIndex}`][0]
            );
            _this.$refs[`VideoPlayer${activeLoopIndex}`][0].player.play();
          }
        },
      });
    },
  },
};
</script>
<style lang="scss" scoped>
.pc-slide {
  width: 500px;
  margin: 0 auto;
}

.view .swiper-container {
  width: 500px;
  height: 500px;
}

.view .arrow-left {
  background: url(index_tab_l.png);
  position: absolute;
  left: 10px;
  top: 50%;
  margin-top: -25px;
  width: 28px;
  height: 51px;
  z-index: 10;
}

.view .arrow-right {
  background: url(index_tab_r.png);
  position: absolute;
  right: 10px;
  top: 50%;
  margin-top: -25px;
  width: 28px;
  height: 51px;
  z-index: 10;
}

.preview {
  width: 100%;
  margin-top: 10px;
  position: relative;
}

.preview .swiper-container {
  width: 430px;
  height: 82px;
  margin-left: 35px;
}

.preview .swiper-slide {
  width: 87px;
  height: 82px;
}

.preview .slide6 {
  width: 82px;
}

.preview .arrow-left {
  background: url(feel3.png);
  position: absolute;
  left: 10px;
  top: 50%;
  margin-top: -9px;
  width: 9px;
  height: 18px;
  z-index: 10;
}

.preview .arrow-right {
  background: url(feel4.png);
  position: absolute;
  right: 10px;
  top: 50%;
  margin-top: -9px;
  width: 9px;
  height: 18px;
  z-index: 10;
}

.preview img {
  padding: 1px;
}

.preview .active-nav img {
  padding: 0;
  border: 1px solid #F00;
}
</style>