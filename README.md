# 站点内使用的banner位
## 引入方式
> 在head区域引入脚本
```
<script
	id="ads-tag-sdk"
	data-zone-id="test"
	src="https://sdk.enjoy4fun.com/v1/ads-tag.js">
</script>
```

### 参数说明
- id: 当前脚本的标识，固定值，必传
- data-zone-id: 域名唯一标识，由管理人员提供
- src: sdk地址

### 渲染广告
- 1.在需要渲染的dom区域绑定id或其它html标识
```html
<div id="test-one"></div>
```
- 2.使用window.adsTag.renderAds进行广告渲染，参数如下:
  - dom: 需要渲染广告的html容器
  - width: 指定广告的宽度
  - height: 指定广告的高度
```javascript
	window.adsTag.renderAds(document.querySelector('#test-one'), 300, 250);
```
