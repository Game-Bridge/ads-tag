# ads Tag Label Management
## Input Method
> First, the adsTag script needs to be input in the head area
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

### Parameter Description

| Parameters   | Type   | Description                                                          | Prerequisite or not |
|--------------|--------|----------------------------------------------------------------------|---------------------|
| id           | string | The tag of the current script, fixed value: `ads-tag-sdk`            | Yes                 |
| data-site-id | string | The unique domain name identification, provided by the administrator | Yes                 |
| data-utm-source  | string | channel ID, its weight factor is higher than utm-source of url parameter.   | No    |
| data-test       | string | Enable Test Mode or Not: Test Mode will be opened when value=on. Caution! Do not use it in Production Environment.           | No    |
| src          | string | sdk address, fixed value: `https://sdk.enjoy4fun.com/v1/ads-tag.js`  | Yes                 |

## Use
### Direct call
```javascript
window.adsTag.renderAds(document.querySelector('#test-one'), 300, 250, zoneId);
```
### Call with `cmd`
If you can’t confirm if adsTag is loaded while using, then it is recommended to call with cmd.
```javascript
window.adsTag.cmd.push(function (){
	window.adsTag.renderAds(document.querySelector('#test-one'), 300, 250, zoneId);
});
```

### Initialization
```javascript
window.adsTag.init({
	// Whether to enable fixed width, false as the default, it is recommended to use the default value to achieve higher benefits
	fixedWidth: true
});
```

### Render ads
#### I. Display Ads `zoneType: Display`
- 1.Designate a dom node as the ad container for renderAds by binding an id or other attribute identifier.
```html
<div id="test-one"></div>
```
- 2.Use`window.adsTag.renderAds(dom, width, height, zoneId)`to render the ads

##### Parameter Description
| Parameters | Type        | Description                                                                                                                                                                                               | Mandatory or not | Default Value |
|------------|-------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|---------------|
| dom        | HtmlElement | Need the container in which the ads are rendered, for a good experience the `width` and `height` of the container should be bigger than or equal to the values set by the parameters of width and height. | Yes              | --            |
| width      | number      | Specify the width of the ads                                                                                                                                                                              | Yes              | --            |
| height     | number      | Specify the height of the ads                                                                                                                                                                             | Yes              | --            |
| zoneId     | string      | Specify the ad unit group, use this parameter to differentiate the ad group revenue                                                                                                                       | Yes              | --            |

##### Example
```javascript
window.adsTag.renderAds(document.querySelector('#test-one'), 300, 250, zoneId);
```


#### II. WebInterstitial Ads `zoneType: WebInterstitial`
Inserting ads don’t need to create a container, the ads are rendered by calling `window.adsTag.renderInterstitial(zoneId, querySelector)`method

##### Parameter Description
| Parameters    | Type   | Description                                                                                                                                                                                                                                                                         | Mandatory or not | Default Value |
|---------------|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|---------------|
| zoneId        | string | Specify the ad unit group, use this parameter to differentiate the ad group revenue                                                                                                                                                                                                 | Yes              | --            |
| querySelector | string | Specifies that the `a` tags matching this selector should use interstitial ads, when the parameter is empty, all a tags will take effect. Selectors are recommended to use `className` or `attribute`, and care is taken to ensure that there are no events that block `href` jumps | No               | --            |

##### Example
```javascript
window.adsTag.renderInterstitial(zoneId);
```

##### Caution
- When this method is called, it only takes effect on the a tag jump in the page
- Can only be called once in a single page, multiple calls are invalid

#### III. Anchor Ads `zoneType: Anchor`
Anchor ads don't need to create a container, ads are rendered by calling `window.adsTag.renderAnchor(zoneId, type)` method

##### Parameter Description
| Parameters | Type   | Description                                                                         | Mandatory or not | Default Value |
|------------|--------|-------------------------------------------------------------------------------------|------------------|---------------|
| zoneId     | string | Specify the ad unit group, use this parameter to differentiate the ad group revenue | Yes              | --            |
| type       | string | Position of the anchored ad, optional values: 'top', 'bottom'                       | No               | 'bottom'      |

##### Example
```javascript
window.adsTag.renderAnchor(zoneId, 'bottom');
```

##### Caution
- Can only be called once in a single page, multiple calls are invalid

#### IV. Reward Ads `zoneType: Reward`
Incentivized ads don't need to create a container, ads are rendered by calling `window.adsTag.renderReward(zoneId, doneFn)` method

##### Parameter Description
| Parameters | Type     | Description                                                                                                              | Mandatory or not | Default Value        |
|------------|----------|--------------------------------------------------------------------------------------------------------------------------|------------------|----------------------|
| zoneId     | string   | Specify the ad unit group, use this parameter to differentiate the ad group revenue                                      | Yes              | --                   |
| doneFn     | function | Incentive ad completion execution function, the parameter `rewardStatus` returns the display status of the incentive ad. | No               | (rewardStatus) => {} |

##### Example
```javascript
window.adsTag.renderReward(zoneId, (rewardedStatus) => {
    if (rewardedStatus) {
	// Execute the incentive ad display after completion of the operation
	} else {
        // Perform Incentive Ad Display Not Completed Action
	}
});
```

##### Caution
- Incentivized ads may display video ads, it is recommended to call this method after the user has generated a page interaction

#### V. Interstitial Ads `zoneType: Interstitial`
Inserted screen ads don't need to create a container, ads are rendered by calling `window.adsTag.adBreak({ zoneId, type, adBreakDone })` method

##### Parameter Description
| Parameters  | Type     | Description                                                                                                                                             | Mandatory or not | Default Value  |
|-------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------------|
| zoneId      | string   | Specify the ad unit group, use this parameter to differentiate the ad group revenue                                                                     | Yes              | --             |
| type        | string   | Specify the type of ad, passable parameters: preroll, midroll, reward                                                                                   | Yes              | --             |
| adBreakDone | function | The function is executed after the advertisement fails or finishes playing, and the parameter `viewed` returns the display status of the advertisement. | No               | (viewed) => {} |

##### Example
```javascript
window.adsTag.adBreak({ zoneId: 'xxx', type: 'midroll', adBreakDone: (viewed) => {
    if (viewed) {
        // Ads Display Successfully
	} else {
        // Failure to display ads, or aborted by the user
	}
}});
```

#### Ⅵ. Sidewall Ads `zoneType: Sidewall`
Sidewall Ads do not need create container. Render it through the instruction from “window.adsTag.renderSidewall(zoneId)”.
##### Parameter Description:
| Parameters | Type   | Description                                                                         | Mandatory or not | Default Value |
|---------|-------------|---------------------------------------|------|--------------------------|
| zoneId  | string      | Specify the ad unit group, use this parameter to differentiate the ad group revenue               | Yes    | --                       |

##### Example:
```javascript
window.adsTag.renderSidewall(zoneId);
```

#### Ⅶ. Fixed Ads `zoneType: Fixed`
Fixed Ads do not need create container. Render it through the instruction from “window.adsTag.renderFixed(zoneId, width, heigth)”.

##### Parameter Description:
| Parameters | Type   | Description                                                                         | Mandatory or not | Default Value |
|--------|---------|------------------------------------|------|-----|
| zoneId | string  | Specify the ad unit group, use this parameter to differentiate the ad group revenue             | Yes    | --  |
| width  | number  | Specify Ads Width. Adjust it according to the actual layout of Web.                | No    | 300 |
| height | number  | Specify Ads Height. Adjust it according to the actual layout of Web.                | No    | 250 |
##### Example:
```javascript
window.adsTag.renderFixed(zoneId);
```


### Example of Ads Effect
#### PC Banner
![pc banner](https://github.com/Game-Bridge/ads-tag/assets/11342827/2a6037fc-ed1a-4485-bbf2-03eb351b421e)

#### PC Interstitial
![pc interstitial](https://github.com/Game-Bridge/ads-tag/assets/11342827/1d581fe1-add1-41fa-9a92-e571d93b3075)

#### Mobile
![mobile](https://github.com/Game-Bridge/ads-tag/assets/11342827/68f20d89-eaa9-498f-933d-7159b56c96c2)

