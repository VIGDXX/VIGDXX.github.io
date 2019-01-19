# Android 自动播放

### Android webview 默认播放策略

> Muted autoplay is always allowed.

> Autoplay with sound is allowed if:
> 1. User has interacted with the domain (click, tap, etc.).
> 2. On desktop, the user's Media Engagement Index threshold has been crossed, meaning the user has previously play video with sound.
> 3. On mobile, the user has [added the site to their home screen].

Top frames can delegate autoplay permission to their iframes to allow autoplay with sound.

[参考资料](https://developers.google.com/web/updates/2017/09/autoplay-policy-changes)

### 修改 Andorid 默认策略
想要实现视频带声音自动播放必须在native层面调用如下方法

```
setMediaPlaybackRequiresUserGesture(false)
```
[参考资料](https://developer.android.com/reference/android/webkit/WebSettings#setMediaPlaybackRequiresUserGesture(boolean))

# iOS 自动播放

### iOS webview 默认播放策略

iOS 9— 必须用户手势， iOS 10+ 新策略：

> <video autoplay> elements will now honor the autoplay attribute, for elements which meet the following conditions:
> 1. <video> elements will be allowed to autoplay without a user gesture if their source media contains no audio tracks.
> 2. <video muted> elements will also be allowed to autoplay without a user gesture.
> 3. If a <video> element gains an audio track or becomes un-muted without a user gesture, playback will pause.
> 4. <video autoplay> elements will only begin playing when visible on-screen such as when they are scrolled into the > viewport, made visible through CSS, and inserted into the DOM.
> 5. <video autoplay> elements will pause if they become non-visible, such as by being scrolled out of the viewport.
  
 想要hack的可以放弃了。。
 
[参考资料](https://webkit.org/blog/6784/new-video-policies-for-ios/)
### 修改 iOS 默认策略
想要实现视频带声音自动播放必须在native层面调用如下方法
```
let configuration = WKWebViewConfiguration()
configuration.allowsInlineMediaPlayback = true
configuration.mediaTypesRequiringUserActionForPlayback = .audio
let webView = WKWebView(frame: .zero, configuration: configuration)
```

[参考资料](https://www.thomasvisser.me/2018/06/26/wkwebview-media/)

# 视频播放时调用协调播放器
```
<video  playsinline webkit-playsinline>
```

