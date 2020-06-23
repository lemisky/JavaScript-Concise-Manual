# 油猴脚本

## 匹配所有网址

```javascript
// @match        *://*/*
```

或者使用

```javascript
// @include      http://*/*
// @include      https://*/*
```

## 导入JQuery库——使Chrome Console支持JQuery

```javascript
// ==UserScript==
// @name         Jquery Support
// @namespace    dev
// @version      0.1.1
// @description  Chrome Dev Console Jquery
// @author       foyou
// @match        *://*/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';
    window.jQuery || JQuery Code
    // Your code here...
})();
```

## Chrome插件

![image-20200328212721631](img/image-20200328212721631.png)

### icon_128.png

![image-20200328212732545](img/image-20200328212732545.png)

### Jqy.js

```javascript
function addJquery() {
    var var_js = document.createElement('script');
    var_js.src = chrome.extension.getURL('jquery-3.4.1.min.js');
    document.getElementsByTagName('head')[0].appendChild(var_js);
}

addJquery();
```

### jquery-3.4.1.min.js

```javascript
window.jQuery || !function(e,t){"use strict"; ...
```

### manifest.json

```json
{
  "name": "DevTools JQuery",
  "version": "0.1",
  "manifest_version": 2,
  "description": "Chrome DevTools Console JQuery",
  "icons": {
    "128": "icon_128.png"
  },
  "content_scripts": [
    {
      "matches": [
        "<all_urls>"
      ],
      "js": ["Jqy.js"]
    }
  ],
  "web_accessible_resources": [
    "jquery-3.4.1.min.js"
  ]
}
```

