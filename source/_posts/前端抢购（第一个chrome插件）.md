---
title: 前端抢购（第一个chrome插件）
date: 2018/01/28 16:30:11
categories:
- Technology
tags:
- Technology
---
# 前言
最近[小爱开放抢购](https://item.mi.com/product/6334.html)，忍不住想去抢一个，苦苦抢不到，于是想写一个抢购脚本，看看效果，于是就有了我的第一个chrome插件。

<!-- more -->

## 开始
我们先审查小米抢购页面的元素，按F12，再抢购开始的时候，小米这个抢购按钮会变为可以点击的状态，我们可以看到这个按钮的id 、class等等信息，如图所示：
![按钮信息](http://ogda5d704.bkt.clouddn.com/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20180128164206.png)
我们就可以拿着这些信息来做模拟点击，我们每隔10毫秒点击一次，可以说是最快的速度去发送请求了，人手点击根本比不了。先写个定时函数，如下所示
```javascript
setInterval(function() {
if(Date.now() >= new Date("2018-01-27 20:00:01")){
document.getElementsByClassName('btn btn-primary  btn-biglarge J_proBuyBtn')[0].click(); 
}
},10);
```
> 时间一过8点钟就进行点击抢购按钮

经过我的测试呢，按钮被点击的时候还有许多意外的情况发生，比如网络错误，网络拥堵，我们还需要把这些意外情况解决了。如下代码
```javascript
setInterval(function() {
if(Date.now() >= new Date("2018-01-28 20:00:01")){
	if (document.getElementsByClassName('modal modal-hide modal-bigtap-queue in').length > 0) {
		if (document.getElementsByClassName('modal modal-hide modal-bigtap-queue in')[0].style.display == "block") {
			console.log('正在排队');
		}
	}
	
	else{
		if (document.getElementsByClassName('modal fade modal-hide modal-bigtap-soldout  modal-bigtap-soldout-norec in').length > 0) {
			document.getElementsByClassName('modal fade modal-hide modal-bigtap-soldout  modal-bigtap-soldout-norec in')[0].childNodes[1].click();
		}

		if (document.getElementById('J_miAlertConfirm')) {
			document.getElementById('J_miAlertConfirm').click();
		}

		if (document.getElementById('J_bigtapRetry')) {
			document.getElementById('J_bigtapRetry').click();
		}

		if (document.getElementsByClassName('modal-backdrop fade in').length > 0) {
			for(var i = 0; i < document.getElementsByClassName('modal-backdrop fade in').length; i++){
				document.getElementsByClassName('modal-backdrop fade in')[i].parentNode.removeChild(document.getElementsByClassName('modal-backdrop fade in')[i]);
			}
		}

		if (document.getElementsByClassName('modal fade modal-hide modal-bigtap-soldout  modal-bigtap-soldout-norec in').length > 1) {
			for(var a = 0; a < document.getElementsByClassName('modal-backdrop fade in').length; a++){
				document.getElementsByClassName('modal fade modal-hide modal-bigtap-soldout  modal-bigtap-soldout-norec in')[a].parentNode.removeChild(document.getElementsByClassName('modal fade modal-hide modal-bigtap-soldout  modal-bigtap-soldout-norec in')[a]);
			}
		}

		if (document.getElementsByClassName('modal fade modal-hide modal-bigtap-soldout  modal-bigtap-soldout-norec').length > 1) {
			for(var a = 0; a < document.getElementsByClassName('modal-backdrop fade in').length; a++){
				document.getElementsByClassName('modal fade modal-hide modal-bigtap-soldout  modal-bigtap-soldout-norec')[a].parentNode.removeChild(document.getElementsByClassName('modal fade modal-hide modal-bigtap-soldout  modal-bigtap-soldout-norec')[a]);
			}
		}

		document.getElementsByClassName('btn btn-primary  btn-biglarge J_proBuyBtn')[0].click(); 
	}
}
else {
	console.log('未开始')
}

},10);
```
> 大部分的解决意外情况的发生，最快的速度进行排队

## 运行
这么代码你只要复制到Console控制台，按下回车就可以运行了。
但是你没刷新一次页面的时候，又要重新复制一遍，很繁琐，怎么解决呢？于是就有了我的第一个chrome插件。

### 配置chrome插件
创建一个文件夹，文件夹的目录结构有manifest.json ，它是配置文件，然后是相对应的js，html，和资源文件，结构图如下所示：
![结构目录](http://ogda5d704.bkt.clouddn.com/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20180128221743.png)

manifest.json 里如下配置：
```javascript
{
	"name":"第一个小米抢购插件",
	"manifest_version":2,
	"version":"1.0",
	"description":"keien的自动抢购插件",
	"browser_action":{
		"default_icon":"logo.png"
	},
	"content_scripts":[
			{
		"matches":["https://item.mi.com/product/*"],
		"js":["mi.js"]
		}
	]
}
```
> 其中name 、manifest_version 、version 是一定要有的
> manifest_version 一定要配置为2 

mi.js 里的代码就是上面在console里输入的代码，图片可以随便一张图片，做到这里，你就成功的配置好了一个插件，接下来就是导入插件了

### 插件的导入与运行
在chrome上打开  更多工具->扩充功能  就可以看到如下界面：
![扩充功能](http://ogda5d704.bkt.clouddn.com/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_1103.png)
选择我们一开始建立好的文件夹，导入，就大功告成了。
### 结果
打开[小爱抢购界面](https://item.mi.com/product/6334.html)，我们在控制台可以看到打印出**未开始**，如下界面
![控制台](http://ogda5d704.bkt.clouddn.com/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87aaa41.png)
你已经成功完成了一个chrome插件，你再次刷新界面，还是会显示**未开始**，再也不用重新在粘贴一次代码了，这就是插件的强大之处，不会被reload掉。
# 最后
此代码仅供参考，如有错误之处，多多指教。
