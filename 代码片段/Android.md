### 数据类型

##### 问题：超长double自动使用科学计数法显示

```java
DecimalFormat df = new DecimalFormat("#");
String string = df.format(double);
```



### 软键盘

##### 收起软键盘

```java
InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);  
imm.toggleSoftInput(0, InputMethodManager.HIDE_NOT_ALWAYS);  
```





