# 广告标签管理
## 引入方式
> 在head区域引入脚本
```
<script
	id="ads-tag-sdk"
	data-site-id="site_11"
	src="https://sdk.enjoy4fun.com/v1/ads-tag.js">
</script>
```

### 参数说明
- id: 当前脚本的标识，固定值，必传
- data-site-id: 域名唯一标识，必传，由管理人员提供
- src: sdk地址

### 渲染广告
#### 1.banner广告
- 1.在需要渲染的dom区域绑定id或其它html标识
```html
<div id="test-one"></div>
```
- 2.使用`window.adsTag.renderAds`进行广告渲染，参数如下:
  - dom: 需要渲染广告的html容器
  - width: 指定广告的宽度
  - height: 指定广告的高度
  - zoneId: 指定广告单元组，使用该参数可以区分广告组收益
  - videoFirst: 指定当前广告单元组优先展示视频，只要存在可用的视频即进行展示。注意: 单个页面仅能指定一次(单个页面同时只允许一个视频处于展示中)
```javascript
window.adsTag.renderAds(document.querySelector('#test-one'), 300, 250, zoneId);
```
### banner广告演示
主要尺寸：728*90
![image](https://user-images.githubusercontent.com/7828841/218071945-a9386dbd-b9f0-4119-8425-eb005149ee3c.png)



#### 2.穿插广告
穿插广告不需要创建容器，通过调用`window.adsTag.renderInterstitial`方法进行广告渲染。需要注意: **单个页面中仅能调用一次**。
```javascript
window.adsTag.renderInterstitial(zoneId);
```
