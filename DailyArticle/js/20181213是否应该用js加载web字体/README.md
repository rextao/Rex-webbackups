# 概述

1. https://www.filamentgroup.com/lab/js-web-fonts.html
2. 20181129
3. 作者认为，许多浏览器中的默认web字体加载行为使得只使用CSS的方法成为页面文本呈现的赌博
4. 浏览器是这样处理自定义字体的，加载字体时，先显示一个“备用”字体，然后加载好了再换掉，不流畅还可能会造成页面布局重新变动

## 读后总结

1. 了解web字体加载历史，现在css加载字体不会存在问题



## 字体加载历史

### 1997年只使用CSS的网页字体很好 

1. ie率先引入web字体，字体加载过程中，回退的文本是可见的（加载字体需要时间-。-）

### 2008提倡用js加载web字体

1. 2008年safari支持web字体
2. 但设计缺陷（加载字体文件时，因此页面text，并未设置请求超时，故如请求出错等情况，页面无内容显示）导致需要使用js方法解决这个问题

### 2016年css-only不那么糟

1. 浏览器都增加字体超时设置，如请求字体超时，则会显示回退文本
2. 但对文本的可见与否的控制并不好

### 2018年css-only good

1. 利用@font-face，[caniuse](https://caniuse.com/#feat=css-font-rendering-controls)查看兼容性（比较差）

2. 在 CSS3 之前，web 设计师必须使用已在用户计算机上安装好的字体，利用@font-face，设计师可以使用自己的字体

	```css
	@font-face{
	    font-family: myFirstFont;
	    src: url('Sansation_Light.ttf'),
	    	 url('Sansation_Light.eot'); /* IE9+ */
	    font-display: swap;/*先显示默认字体，web字体加载后替换*/
	}
	div{
		font-family:myFirstFont;
	}
	```

## 为何还需要使用js

## 重绘

1. @font-face包含多个字体文件，每个请求可能引起页面的重绘和回流 

2. 可以用js解决这个问题，利用promise请求完后一起添加到fonts中

	```javascript
	if ("fonts" in document) {
	  var font = new FontFace(
	    "Noto Serif",
	    "url(notoserif.woff2) format('woff2'), url(notoserif.woff) format('woff')"
	  );
	  var fontBold = new FontFace(
	    "Noto Serif",
	    "url(notoserif-bold.woff2) format('woff2'), url(notoserif-bold.woff) format('woff')",
	    { weight: "700" }
	  );
	  Promise.all([
	    font.load(),
	    fontBold.load()
	  ]).then(function(loadedFonts) {
	    // Render them at the same time
	    loadedFonts.forEach(function(font) {
	      document.fonts.add(font);
	    });
	  });
	}
	```

## 使用用户偏好

1. 