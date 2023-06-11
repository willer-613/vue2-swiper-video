<template>
  <div class="pc-slide">
    <div class="view">
      <div class="swiper-container">
        <a class="arrow-left" href="#" v-if="leftIcoB">
          <img :src="leftIcoB">
        </a>
        <a class="arrow-right" href="#" v-if="rightIcoB">
          <img :src="rightIcoB">
        </a>
        <div class="swiper-wrapper">
          <div
            class="swiper-slide"
            :class="{'active-nav':index===0}"
            v-for="pic,index in pics"
            :key="index"
          >
            <a :href="pic.href" target="_blank" v-if="pic.href">
              <img :src="pic.big" alt>
            </a>
            <img :src="pic.big" alt v-else>
          </div>
        </div>
      </div>
    </div>
    <div class="preview">
      <a class="arrow-left" href="#" v-if="leftIcoS">
        <img :src="leftIcoS">
      </a>
      <a class="arrow-right" href="#" v-if="rightIcoS">
        <img :src="rightIcoS">
      </a>
      <div class="swiper-container">
        <div class="swiper-wrapper">
          <div
            class="swiper-slide"
            :class="{'active-nav':index===0}"
            v-for="pic,index in pics"
            :key="index"
          >
            <img :src="pic.small" alt>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "Swiper",
  props: {
    jqueryImportType: {
      type: String
    },
    jqueryObj: {
      type: Object
    },
    pics: {
      type: Array,
      default() {
        return [
          {
            big: "", //大图
            small: "", //小图
            href: "" //点击大图跳转链接
          }
        ];
      }
    },
    //左滚动图标 大
    leftIcoB: {
      type: [String, Object]
    },
    //右滚动图标 大
    rightIcoB: {
      type: [String, Object]
    },
    //左滚动图标 小
    leftIcoS: {
      type: [String, Object]
    },
    //右滚动图标 小
    rightIcoS: {
      type: [String, Object]
    }
  },
  data() {
    return {
      viewSwiper: null,
      previewSwiper: null
    };
  },
  watch: {
    pics(val) {
      this.$nextTick(() => {
        this.init();
      });
    }
  },
  methods: {
    init() {
      this.viewSwiper = null;
      this.previewSwiper = null;

      let viewSwiper = (this.viewSwiper = new window.Swiper(
        ".view .swiper-container",
        {
          onSlideChangeStart: function() {
            updateNavPosition();
          }
        }
      ));
      let previewSwiper = (this.previewSwiper = new window.Swiper(
        ".preview .swiper-container",
        {
          visibilityFullFit: true,
          slidesPerView: "auto",
          onlyExternal: true,
          onSlideClick: function() {
            viewSwiper.swipeTo(previewSwiper.clickedSlideIndex);
          }
        }
      ));

      let jquery;
      if (this.jqueryImportType === "script") {
        jquery = window.$;
      } else {
        jquery = this.jqueryObj;
      }
      jquery(".view .arrow-left,.preview .arrow-left").on("click", e => {
        e.preventDefault();
        if (viewSwiper.activeIndex === 0) {
          viewSwiper.swipeTo(this.pics.length - 1, 1000);
          return;
        }
        viewSwiper.swipePrev();
      });
      jquery(".view .arrow-right,.preview .arrow-right").on("click", e => {
        e.preventDefault();
        if (viewSwiper.activeIndex === viewSwiper.slides.length - 1) {
          viewSwiper.swipeTo(0, 1000);
          return;
        }
        viewSwiper.swipeNext();
      });

      function updateNavPosition() {
        window.$(".preview .active-nav").removeClass("active-nav");
        var activeNav = window
          .$(".preview .swiper-slide")
          .eq(viewSwiper.activeIndex)
          .addClass("active-nav");
        if (!activeNav.hasClass("swiper-slide-visible")) {
          if (activeNav.index() > previewSwiper.activeIndex) {
            var thumbsPerNav =
              Math.floor(previewSwiper.width / activeNav.width()) - 1;
            previewSwiper.swipeTo(activeNav.index() - thumbsPerNav);
          } else {
            previewSwiper.swipeTo(activeNav.index());
          }
        }
      }
    }
  },
  mounted() {
    this.init();
  }
};
</script>
<style scoped>
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