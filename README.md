# 站点内使用的banner位
## 引入方式
> 在head区域引入脚本
```
<script
	id="ads-tag-sdk"
	data-site-id="site_11"
	data-zone-id="zone_1"
	src="https://sdk.enjoy4fun.com/v1/ads-tag.js">
</script>
```

### 参数说明
- id: 当前脚本的标识，固定值，必传
- data-site-id: 域名唯一标识，非必传，由管理人员提供
- data-zone-id: 广告默认单元组，非必传，通过renderAds进行单独配置，由管理人员提供
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
  - zoneId: 指定广告单元组，如未指定，将使用script的data-zone-id属性做为默认值(使用该参数可以区分广告组收益)
```javascript
	window.adsTag.renderAds(document.querySelector('#test-one'), 300, 250, zoneId);
```
