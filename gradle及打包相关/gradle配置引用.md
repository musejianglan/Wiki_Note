> project中多个module某些配置参数（编译版本等）相同，为了统一管理，将相同的参数放到同一个文件中管理

### 在project中新建config.gradle文件
ext {

    externalPagerSlidingTabStrip = 'com.astuetz:pagerslidingtabstrip:1.0.1'

    externalEasyPermissions = 'pub.devrel:easypermissions:0.2.1'

    externalJunit = 'junit:junit:4.12'

    externalCompileSdkVersion = 27
    externalBuildToolsVersion = "27.0.0"
    externalMinSdkVersion = 16
    externalTargetSdkVersion = 27
}

### 在project build.gradle中添加 apply from: 'config.gradle'

这样在同一个project的所有build.gradle中均可以引用config.gradle中的参数

```
		minSdkVersion externalMinSdkVersion
        targetSdkVersion externalTargetSdkVersion
```
