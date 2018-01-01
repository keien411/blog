---
title: Andfix 踩坑记录
---
# 前言
刚看到android热更新，抱着好奇心去玩了一把，没想到有这多的坑啊，记录下坑！

## 踩坑
1. 加权限，我在这里爬了很久，愣是没想起来

```
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>

<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```

2. 它仅仅支持修改类的方法（新增类，新增字段都是不可以的），你修改的地方一定要在方法里面，也不行在点击事件里，在点击事件里也要是在    方法里修改。一定要在方法里，一定要在方法里，一定要在方法里。

![andfix原理](http://upload-images.jianshu.io/upload_images/2566179-3e66d5fff2b8ae52.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

    就像下面一样，修改要放在fix()方法里。
    
![修改在fix()里](http://upload-images.jianshu.io/upload_images/2566179-3e17e8bbab3c0d47.png)


# 最后
AndFix就像朴实的劳动人民，就是来修bug的不要找我来搞事情。

以后有时间去看下Tencent/tinker。

