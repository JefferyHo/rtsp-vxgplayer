# 《浏览器播放RTSP方案》之 VXGPlayer插件播放RTSP视频流

## VXGPlayer插件播放RTSP视频流
总体来说vxgplayer是付费插件，更多支持的功能可以去官网详询。作为一个demo研究，检索资料和实现总结如下：

## 环境搭建

 别人有一篇文章总结的很好，就不赘述。直接上链接 [整合vxgPlayer使chrome支持vxg_media_player播放rtsp视频](https://blog.csdn.net/qq_34817440/article/details/105644393)


> 关于如何安装多chrome浏览器, 可以参考我的另一篇 [VLC插件播放RTSP视频流-多版本chrome安装](https://blog.csdn.net/sinat_36065456/article/details/119737236?spm=1001.2014.3001.5501)

## 实例代码 

```
// 项目目录
// │  index.html
// └─lib
//     media_player.nmf
//     media_player.pexe
//     vxgplayer-1.8.40.min.css
//     vxgplayer-1.8.40.min.js

// 完整代码
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>测试video 视频资源获取与播放</title>
  <script type="text/javascript" src="./lib/vxgplayer-1.8.40.min.js"></script>
  <link rel="stylesheet" href="./lib/vxgplayer-1.8.40.min.css">
</head>
<body>
  <div class="test-page">
    <span> 测试video 视频资源获取与播放</span>
    <div onclick="playVideo()" class="btn-vis">点击播放视频</div>
    <div class="video-warp" v-show="videoWarpShow">
      <div onclick="closeV()" class="close">x</div>
      <div class="vxgplayer" id="vxg_media_player1" url="" aspect-ratio latency="10" 
        autostart controls avsync nmf-src="./lib/media_player.nmf" nmf-path="media_player.nmf"
        width="600" height="600">
      </div>
    </div>
  </div>
  <script>
    function closeV() {
      window.vxgplayer('vxg_media_player1').stop();
    }

    function playVideo() {
      window.vxgplayer('vxg_media_player1').stop();
      window.vxgplayer('vxg_media_player1').src("wowzaec2demo.streamlock.net/vod/mp4:BigBuckBunny_115k.mov");
      window.vxgplayer('vxg_media_player1').play();
    }
  </script>
</body>
</html>

```

## 问题
1. 视频分辨率为2560时，播放3秒后卡顿，且不会自行恢复
2. logo目前去不掉（付费版可以），官网 https://www.videoexpertsgroup.com/
3. 之前用1.8.2的时候播放1080p的视频也会卡住，换1.8.40就不会

## 最后

虽然项目没用上，但是写了一个简单的vue组件，也分享给大家。happy coding~