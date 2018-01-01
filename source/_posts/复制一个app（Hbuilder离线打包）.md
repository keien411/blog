---
title: 复制一个app（Hbuilder离线打包）
---
# 前言
```
        客户的要求，真是......还是记录下复制步骤，要加的东西太多，好记性不如烂笔头啊
```
## 粘贴复制重命名

1. 打开androidstudio导入项目，修改它的包名，名称

2. 根据包名申请各种第三方（facebook,twitter,个推，友盟，googleanalytics）

3. 修改string里的facebook和twitter的第三方参数（已有注释）

4. 在AndroidManfest.xml修改facebook分享的值

![facebook分享](http://ogda5d704.bkt.clouddn.com/fuzhi1.png)

5. 在AndroidManfest.xml修改个推的值AppID（3）AppSecret（1）AppKey（1）

6. 在AndroidManfest.xml修改包名，替换所有的文件

![facebook分享](http://ogda5d704.bkt.clouddn.com/fuzhi2.png)

7. 在AndroidManfest.xml修改友盟的value

8. 配置 googleanalytics 下载相应的google-server.json，放在app目录下

9. 修改res/xml/ecommerce_tracker.xml 里的 ga_trackingId 的值

# 最后
```
        还有各种资源图片的修改，（不写了）
```


