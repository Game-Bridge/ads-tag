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

#### 2.穿插广告
穿插广告不需要创建容器，通过调用`window.adsTag.renderInterstitial`方法进行广告渲染, 参数如下:
- zoneId: 指定广告单元组，使用该参数可以区分广告组收益
- querySelector: 指定拥有该选择器的a标签使用穿插广告, 不指定则为全部a标签生效，可以使用className或attribute
```javascript
// 需要注意: **单个页面中仅能调用一次**。
window.adsTag.renderInterstitial(zoneId);
```

### 3.banner广告示例
#### Pc		
![pc banner](https://user-images.githubusercontent.com/7828841/218078481-50a198ed-6b62-4be7-b115-24c0e51de63c.png)
![未命名文件 (1)](https://user-images.githubusercontent.com/7828841/218077274-6a621d56-1d0b-4eac-a0de-6137011c3007.png)
#### Mobile
![mobile-banner](https://user-images.githubusercontent.com/7828841/218080124-8f3284eb-8eeb-4189-84d0-cdb16bb1210c.png)
![mobile-intestital (1)](https://user-images.githubusercontent.com/7828841/218080408-e26d1ce0-8166-4bdf-89c1-fd07aac59432.png)
