<template>
  <div
    class="vxgplayer"
    :id="id"
    :url="url"
    autostart
    avsync
    aspect-ratio
    nmf-src="/vxgplayer/media_player.nmf"
    nmf-path="media_player.nmf"
  ></div>
</template>

<script>
export default {
  name: 'VxgPlayer',
  props: {
    url: {
      type: String,
      default: '',
    },
  },
  data() {
    return {
      id: `vxg_media_player_${new Date().getTime()}`,
    };
  },
  methods: {
    playVideo() {
      // 设置url 播放 ---添加到事件队列在下一个tick执行，避免 TypeError: t.module.postMessage is not a function
      this.$nextTick(() => {
        window.vxgplayer(this.id).stop();
        window
          .vxgplayer(this.id)
          .src(this.url);
        window.vxgplayer(this.id).play();
      });
    },
  },
  mounted() {
    this.playVideo();
  },
  destroy() {
    window.vxgplayer(this.id).dispose();
  },
};
</script>

<style scoped>
.vxgplayer {
  width: 100% !important;
  height: 100% !important;
  margin: 0;
  border: 0;
  box-shadow: none;
}
</style>
