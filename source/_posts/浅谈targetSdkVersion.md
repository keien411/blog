---
title: 浅谈targetSdkVersion
---
- 在app/build.gradle中有个参数targetSdkVersion，标志着应用打包出来的版本

- 如果targetSdkVersion<23,那么android6.0（SDK23）的新特性就不用去适配了（动态申请权限），这个与你手机上的android版本无关，比如可以在android7.0的手机上安装targetSdkVersion=22的应用，这个应用可以不用去动态申请权限。
你不想适配6.0或者7.0，那么就把targetSdkVersion设置为22（5.1）。

- 在targetSdkVersion<23的情况下，该怎么判断有没有权限呢？

```
 public static boolean checkPermission(Context content, String permission){
       boolean result = true;
       
       int targetSdkVersion;
       try {
            final PackageInfo info = content.getPackageManager().getPackageInfo(
                    content.getPackageName(), 0);
            targetSdkVersion = info.applicationInfo.targetSdkVersion;
        } catch (PackageManager.NameNotFoundException e) {
            e.printStackTrace();
        }

        if (targetSdkVersion >= Build.VERSION_CODES.M) {
                    result = content.checkSelfPermission(permission)
                            == PackageManager.PERMISSION_GRANTED;
                } else {
                    result = PermissionChecker.checkSelfPermission(content, permission)
                            == PermissionChecker.PERMISSION_GRANTED;
                }
  return result;
}

```
