```
把.so直接放在JNIlibs目录下.
如果不放默认目录，需要加这个
sourceSets { 
  main { 
      jniLibs.srcDirs = ['目录名字'] 
      } 
  }
```
