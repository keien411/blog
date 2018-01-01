---
title: 插件的简单配置（Hbuilder）
---
```
    今天重新捡起插件归纳下步骤，俗话说好记性不如烂笔头，不要相信自己的记性有多好。有错误之处感谢指出
```
# 前言

```
    首先得有离线打包吧，我用的是Webview集成方式。各种打包方式转下走
```

[Android集成5+SDK的几种方式的应用场景](http://ask.dcloud.net.cn/article/756)
## google analytice为例子

1.在js层新建一个xxx.js,我这里取名为googleanalytice,js

``` js
document.addEventListener("plusready", function() {
    var _BARCODE = 'googleanalytics',
        B = window.plus.bridge;
    var googleanalytics = {
        googleanalyticstest: function(successCallback, errorCallback) {
            var success = typeof successCallback !== 'function' ? null : function(args) {
                    successCallback(args);
                },
                fail = typeof errorCallback !== 'function' ? null : function(code) {
                    errorCallback(code);
                };
            callbackID = B.callbackId(success, fail);
            return B.exec(_BARCODE, "googleanalyticstest", [callbackID]);
        }
    };
    window.plus.googleanalytics = googleanalytics;
}, true);
```

> 这里面有几个参数要说明下googleanalytics，这个要对应这2中feature的name一致
> googleanalyticstest要和3中的方法名一致

2.在assets目录下的data目录下的properties.xml加上这句话

`<feature name="googleanalytics" value="cn.org.GoogleAnalytics.GoogleAnalytics" />`

3.在2中可以看到feature下的value值，它对应着java类，我这边写的是

``` java
public class GoogleAnalytics extends StandardFeature {
    public void googleanalyticstest(final IWebview pWebview, final JSONArray array){
        Intent intent = new Intent(pWebview.getActivity(),AnalyticsCeshi.class);
        pWebview.getActivity().startActivityForResult(intent, 1);
    }
}
```

> 我这里写了个跳转，可以直接在googleanalyticstest写逻辑代码，我比较喜欢在跳转一次到Activity里写逻辑，所以我的逻辑写在AnalyticsCeshi.java里，Activity别忘记在androidmainfest里声明。

4.最后在哪里调用就写上
`plus.googleanalytics.googleanalyticstest();`

> 别忘记引入js文件
# 最后

 就想到这么多了，有错误之处感谢指出。
