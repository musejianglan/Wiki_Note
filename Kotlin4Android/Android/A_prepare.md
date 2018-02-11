Android studio3.0之后自动支持Kotlin，选中支持后自动配置完成。

Project：build.gradle

```
buildscript {

    ext.kotlin_version = '1.1.51'
    ext.anko_version = '0.8.2'
    
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.0.1'
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"//kotlin新增的，添加kotlin支持
        

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        google()
        jcenter()
    }
}
```

module:build.gradle

```

apply plugin: 'kotlin-android'//必须
apply plugin: 'kotlin-android-extensions'//快捷的findviewfindid操作，建议加上

android{
	sourceSets {
        main.java.srcDirs += 'src/main/kotlin'
    }
}

dependencies {
	compile "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"
    compile "org.jetbrains.anko:anko-common:$anko_version"
}
```
