# 广告标签管理
## 引入
> 首先，需要在head区域引入adsTag脚本
```
<script>
	window.adsTag = window.adsTag || { cmd: [] };
</script>
<script
	id="ads-tag-sdk"
	data-site-id="site_11"
	src="https://sdk.enjoy4fun.com/v1/ads-tag.js">
</script>
```

## 使用
### 直接调用
```javascript
window.adsTag.renderAds(document.querySelector('#test-one'), 300, 250, zoneId);
```
### 使用`cmd`调用
如果在使用时不能确认adsTag是否已加载，那么推荐使用`cmd`方式进行调用。
```javascript
window.adsTag.cmd(function (){
	window.adsTag.renderAds(document.querySelector('#test-one'), 300, 250, zoneId);
});
```

### 初始化
```javascript
window.adsTag.init({
	// 是否启用固定宽度, 默认为false，建议使用默认值以达到更高的收益
	fixedWidth: true,
	
	// 广告展示或刷新前事件: 返回是否展示本次广告, 非必传
	refreshBefore: () => {
		// 执行需要在广告展示前的代码
		return true;
	}
});
```

### 参数说明

| 参数      | 类型     | 说明                                             | 是否必传 |
|---------|--------|------------------------------------------------|------|
| id  | string | 当前脚本的标识，固定值为: `ads-tag-sdk`                                | 是    |
| data-site-id  | string | 域名唯一标识，由管理人员提供                                 | 是    |
| src  | string | sdk地址，固定值为: `https://sdk.enjoy4fun.com/v1/ads-tag.js` | 是    |

### 渲染广告
#### 一. Display广告
- 1.通过绑定id或其它属性标识，将某个dom节点指定为`renderAds`所需的广告容器
```html
<div id="test-one"></div>
```
- 2.使用`window.adsTag.renderAds(dom, width, height, zoneId)`进行广告渲染

##### 参数说明:
| 参数      | 类型          | 说明                                                   | 是否必传 | 默认值  |
|---------|-------------|------------------------------------------------------|---|------|
| dom     | HtmlElement | 需要渲染广告的容器, 良好的体验需要该容器的宽高大于或等于参数`width`,`height`所设置的值 | 是 | --   |
| width   | number      | 指定广告的宽度                                              | 是 | --   |
| height   | number      | 指定广告的高度                                              | 是 | --   |
| zoneId  | string      | 指定广告单元组，使用该参数可以区分广告组收益                               | 是 | --   |

##### 示例:
```javascript
window.adsTag.renderAds(document.querySelector('#test-one'), 300, 250, zoneId);
```


#### 二. 穿插广告
穿插广告不需要创建容器，通过调用`window.adsTag.renderInterstitial(zoneId, querySelector)`方法进行广告渲染

##### 参数说明:
| 参数      | 类型          | 说明                                                                                          | 是否必传 | 默认值 |
|---------|-------------|---------------------------------------------------------------------------------------------|------|-----|
| zoneId  | string      | 指定广告单元组，使用该参数可以区分广告组收益                                                                      | 是    | --  |
| querySelector  | string      | 指定匹配该选择器的a标签使用穿插广告, 参数为空时全部`a`标签都会生效。选择器建议使用`className`或`attribute`，并注意保证不存在阻挡`href`跳转的事件 | 否    | -- |

##### 示例:
```javascript
window.adsTag.renderInterstitial(zoneId);
```

##### 注意事项: 
- 该方法调用后，仅对页面中的a标签跳转生效
- 单个页面中仅能调用一次，多次调用无效

#### 三. 锚定广告
锚定广告不需要创建容器，通过调用`window.adsTag.renderAnchor(zoneId, type)`方法进行广告渲染

##### 参数说明:
| 参数      | 类型          | 说明                                                        | 是否必传 | 默认值      |
|---------|-------------|-----------------------------------------------------------|------|----------|
| zoneId  | string      | 指定广告单元组，使用该参数可以区分广告组收益  | 是    | --       |
| type  | string      | 锚定广告的位置，可选值: 'top', 'bottom' | 否    | 'bottom' |

##### 示例:
```javascript
window.adsTag.renderAnchor(zoneId, 'bottom');
```

##### 注意事项:
- 单个页面中仅能调用一次，多次调用无效

#### 四. 激励广告
激励广告不需要创建容器，通过调用`window.adsTag.renderReward(zoneId, doneFn)`方法进行广告渲染

##### 参数说明:
| 参数      | 类型          | 说明                                                        | 是否必传 | 默认值      |
|---------|-------------|-----------------------------------------------------------|------|----------|
| zoneId  | string      | 指定广告单元组，使用该参数可以区分广告组收益  | 是    | --       |
| doneFn  | function | 激励广告完成执行函数，参数`rewardStatus`返回激励广告的展示状态 | 否    | (rewardStatus) => {} |

##### 示例:
```javascript
window.adsTag.renderReward(zoneId, (rewardedStatus) => {
    if (rewardedStatus) {
	// 执行激励广告展示完成后操作
	} else {
        // 执行激励广告展示未完成操作
	}
});
```

##### 注意事项:
- 激励广告可能展示视频广告，建议在用户产生页面交互之后再调用该方法

#### 五. 插屏广告
插屏广告不需要创建容器，通过调用`window.adsTag.adBreak({ zoneId, type, adBreakDone })`方法进行广告渲染

##### 参数说明:
| 参数      | 类型          | 说明                                    | 是否必传 | 默认值                      |
|---------|-------------|---------------------------------------|------|--------------------------|
| zoneId  | string      | 指定广告单元组，使用该参数可以区分广告组收益                | 是    | --                       |
| type  | string      | 指定广告类型，可传参数: preroll, midroll, reward | 是    | --                       |
| adBreakDone  | function | 插屏广告失败或完成播放后执行函数，参数`viewed`返回广告的展示状态  | 否    | (viewed) => {} |

##### 示例:
```javascript
window.adsTag.adBreak({ zoneId: 'xxx', type: 'midroll', adBreakDone: (viewed) => {
    if (viewed) {
        // 广告成功展示
	} else {
        // 广告展示失败，或由用户中止
	}
}});
```

### 广告效果示例
#### Display Pc		
![pc banner](https://user-images.githubusercontent.com/7828841/218078481-50a198ed-6b62-4be7-b115-24c0e51de63c.png)
![未命名文件 (1)](https://user-images.githubusercontent.com/7828841/218077274-6a621d56-1d0b-4eac-a0de-6137011c3007.png)
#### Display Mobile
![mobile-banner](https://user-images.githubusercontent.com/7828841/218080124-8f3284eb-8eeb-4189-84d0-cdb16bb1210c.png)
![mobile-intestital (1)](https://user-images.githubusercontent.com/7828841/218080408-e26d1ce0-8166-4bdf-89c1-fd07aac59432.png)
