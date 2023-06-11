<template>
  <div class="video_box">
    <video ref="videoPlayer" class="video-js" :poster="videoInit.poster">
      <source :src="videoInit.src" :type="videoInit.type" />
    </video>
  </div>
</template>

<script>
import Video from "video.js";
import "video.js/dist/video-js.min.css";

export default {
  name: "VideoPlayer",
  props: {
    videoInit: {
      type: Object,
      default: () => ({}),
    },
  },
  data() {
    return {
      player: null,
    };
  },
  mounted() {
    // 播放参数
    const options = {
      controls: true, // 是否显示底部控制栏
      preload: "auto", // 加载<video>标签后是否加载视频
      autoplay: "muted", // 静音播放
      width: "640",
      height: "247",
      controlBar: {
        // 自定义按钮的位置
        children: [
          {
            name: "playToggle",
          },
          {
            name: "progressControl",
          },
          {
            name: "currentTimeDisplay",
          },
          {
            name: "timeDivider",
          },
          {
            name: "durationDisplay",
          },

          {
            name: "volumePanel", // 音量调整方式横线条变为竖线条
            inline: false,
          },
          {
            name: "pictureInPictureToggle", //画中画播放模式
          },
          {
            name: "fullscreenToggle",
          },
        ],
      },
    };

    console.log(this.$refs, "this.$refs");

    this.player = Video(
      this.$refs.videoPlayer,
      options,
      function onPlayerReady() {
        console.log("onPlayerReady", this);
      }
    );
    console.log(this.player, "this.player");
  },
  beforeDestroy() {
    if (this.player) {
      this.player.dispose();
    }
  },
  methods: {},
};
</script>

<style scoped>
.video_box {
  margin: 10px;
  width: 99%;
  height: 450px;
}
.video-js {
  width: 100%;
  height: 450px;
}
</style>