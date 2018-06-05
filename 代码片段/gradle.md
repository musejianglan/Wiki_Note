```
根据组件名排除或者根据包名排除，下面以排除support-v4库为例：

dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile("com.jude:easyrecyclerview:$rootProject.easyRecyclerVersion") {
        exclude module: 'support-v4'//根据组件名排除
        exclude group: 'android.support.v4'//根据包名排除
    }
}
```

```
if (isModule.toBoolean()) {
    apply plugin: 'com.android.application'
} else {
    apply plugin: 'com.android.library'
}

android {
    compileSdkVersion 27
    defaultConfig {
        if (isModule.toBoolean()) {
            applicationId "包名"
        }

        minSdkVersion 15
        targetSdkVersion 27
        versionCode 1
        versionName "1.0"

        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"

    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }

    sourceSets {
        main {
            if (isModule.toBoolean()) {
                manifest.srcFile 'src/main/AndroidManifest.xml'
            } else {
                manifest.srcFile 'src/main/release/AndroidManifest.xml'
                java{
                    exclude 'debug/**' 
                    //src/main/java/debug  存放启动页和application
                }
            }
        }
    }

}

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])

    implementation 'com.android.support:appcompat-v7:27.1.1'
    implementation 'com.android.support.constraint:constraint-layout:1.1.0'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'com.android.support.test:runner:1.0.2'
    androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'
}

```



第一种

```
config.gradle

ext {

    externalPagerSlidingTabStrip = 'com.astuetz:pagerslidingtabstrip:1.0.1'

    externalEasyPermissions = 'pub.devrel:easypermissions:0.2.1'

    externalJunit = 'junit:junit:4.12'

    externalCompileSdkVersion = 27
    externalBuildToolsVersion = "27.0.0"
    externalMinSdkVersion = 16
    externalTargetSdkVersion = 27
}

---------------------------
buide.gradle

buildscript {

	apply from: 'config.gradle'

    repositories {
        google()
        jcenter()
    }
    
    dependencies {
        classpath 'com.android.tools.build:gradle:3.0.1'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}
--------------------------

 		minSdkVersion externalMinSdkVersion
        targetSdkVersion externalTargetSdkVersion
        
        dependencies {

            compile fileTree(include: ['*.jar'], dir: 'libs')
            testImplementation externalJunit
            compile externalGSON
            compile externalAndroidAppCompatV7
            compile externalAndroidDesign
            compile externalAndroidMultiDex
            compile externalAndroidRecyclerView
            compile externalAndroidSupportV4


        }




```

第二种

```
buide.gradle
buildscript {
    repositories {
        jcenter()
        mavenCentral()
    }

    dependencies {
        //classpath "com.android.tools.build:gradle:$localGradlePluginVersion"
        //$localGradlePluginVersion是gradle.properties中的数据
        classpath "com.android.tools.build:gradle:$localGradlePluginVersion"
    }
}

allprojects {
    repositories {
        jcenter()
        mavenCentral()
        //Add the JitPack repository
        maven { url "https://jitpack.io" }
        //支持arr包
        flatDir {
            dirs 'libs'
        }
    }
}

task clean(type: Delete) {
    delete rootProject.buildDir
}

// Define versions in a single place
//时间：2017.2.13；每次修改版本号都要添加修改时间
ext {
    // Sdk and tools
    //localBuildToolsVersion是gradle.properties中的数据
    buildToolsVersion = localBuildToolsVersion
    compileSdkVersion = 25
    minSdkVersion = 16
    targetSdkVersion = 25
    versionCode = 1
    versionName = "1.0"
    javaVersion = JavaVersion.VERSION_1_8

    // App dependencies version
    supportLibraryVersion = "25.3.1"
    retrofitVersion = "2.1.0"
    glideVersion = "3.7.0"
    loggerVersion = "1.15"
    eventbusVersion = "3.0.0"
    gsonVersion = "2.8.0"
    photoViewVersion = "2.0.0"

    //需检查升级版本
    annotationProcessor = "1.1.7"
    routerVersion = "1.2.2"
    easyRecyclerVersion = "4.4.0"
    cookieVersion = "v1.0.1"
    toastyVersion = "1.1.3"
}
-------------------------------------------

compileSdkVersion rootProject.ext.compileSdkVersion
    buildToolsVersion rootProject.ext.buildToolsVersion

    defaultConfig {
        minSdkVersion rootProject.ext.minSdkVersion
        targetSdkVersion rootProject.ext.targetSdkVersion
        versionCode rootProject.ext.versionCode
        versionName rootProject.ext.versionName
    }
    
	compile "com.android.support:appcompat-v7:$rootProject.supportLibraryVersion"
    compile "com.android.support:design:$rootProject.supportLibraryVersion"
    compile "com.android.support:percent:$rootProject.supportLibraryVersion"
```

