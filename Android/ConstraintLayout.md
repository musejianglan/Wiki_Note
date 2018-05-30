### 控件如何确定自己的位置

##### 1.直接确定控件左上角的坐标

```xml
tools:layout_editor_absoluteX="164dp"
tools:layout_editor_absoluteY="263dp"
```

这二个属性只是单纯的进行演示，在真机操作的时候是无效的，就像"tools:text"一样，可以在写布局的时候方便查看TextView显示的文字，但是实际运行app的时候不会有相应内容。 

##### 2.告诉控件相邻的二个边的位置情况

最简单的基本操作： **app:layout_constraint[自己位置]_[目标位置]="[目标ID|parent]"** 

```
layout_constraintLeft_toLeftOf
layout_constraintLeft_toRightOf
layout_constraintRight_toLeftOf
layout_constraintRight_toRightOf
layout_constraintTop_toTopOf
layout_constraintTop_toBottomOf
layout_constraintBottom_toTopOf
layout_constraintBottom_toBottomOf
layout_constraintBaseline_toBaselineOf
layout_constraintStart_toEndOf
layout_constraintStart_toStartOf
layout_constraintEnd_toStartOf
layout_constraintEnd_toEndOf
```

### Margin值相关

```
android:layout_marginStart
android:layout_marginEnd
android:layout_marginLeft
android:layout_marginTop
android:layout_marginRight
android:layout_marginBottom

```



![ConstraintLayout_margin_gone.png](https://github.com/musejianglan/Wiki_Note/blob/master/img/ConstraintLayout_margin_gone.png)

但是如果我的需求就是A隐藏后，B还是在这个位置（当然有些人可能会说你可以让B根据其他控件来确定位置），而且我的B的位置就是根据A来确定的。那我们怎么处理，我们可以设置B的以下属性，就是当A处于`gone`的时候，我们可以让B的margin值是根据以下的属性值 



```
layout_goneMarginStart
layout_goneMarginEnd
layout_goneMarginLeft
layout_goneMarginTop
layout_goneMarginRight
layout_goneMarginBottom


```

### 位置约束不止二个边

```
<android.support.constraint.ConstraintLayout ...>
    <Button android:id="@+id/button" ...
     app:layout_constraintLeft_toLeftOf="parent"
     app:layout_constraintRight_toRightOf="parent/>
     
<android.support.constraint.ConstraintLayout/>

```

我们让按钮的左边与父布局的左边对齐，让按钮的右边与父布局的右边对齐。这时候因为不是单纯的一边对齐，而是相同直线上的二个边都被约束了。所以按钮无法紧靠着左边的或者右边的其中一个边界，所以这时候，这个按钮就会居于二个约束边界的中间位置。 

如果想让在这二个约束条件下时候不是处于正中间，而是处于左边三分之一的位置，这时候你可以使用： 

```
layout_constraintHorizontal_bias
layout_constraintVertical_bias
分别是水平和垂直方向上的所占比例。
```

### 圆形布局

需求我们可能需要让控件以某个控件为中心，绕着进行布局，如下图所示： 

![ConstraintLayout_1.png.png](https://github.com/musejianglan/Wiki_Note/blob/master/img/ConstraintLayout_1.png)

ConstarintLayout自带了这些功能，我们可以使用： 

```
layout_constraintCircle : 引用另一个控件的id
layout_constraintCircleRadius : 距离另外一个控件中心的距离
layout_constraintCircleAngle : 应该在哪个角度(从0到360度)
```

 

### 尺寸限制（Dimensions constraints）

##### 1.对ConstraintLayout进行限制：

 您可以为ConstraintLayout本身定义最小和最大尺寸：

```
android：minWidth设置布局的最小宽度
android：minHeight设置布局的最小高度
android：maxWidth设置布局的最大宽度
android：maxHeight设置布局的最大高度
```

这些最小和最大尺寸将在ConstraintLayout使用

 ##### 2.对内部的控件进行限制：

可以通过以3种不同方式设置`android：layout_width`和`android：layout_height`属性来指定控件的尺寸：

- 用特定的值（如123dp等）
- 使用WRAP_CONTENT，它会要求控件计算自己的大小
- 使用0dp，相当于“MATCH_CONSTRAINT”

**WRAP_CONTENT（在1.1中添加）** 

 如果设置为WRAP_CONTENT，则在1.1之前的版本中， 约束不会限制生成的尺寸值。但是在某些情况下，您可能需要使用WRAP_CONTENT，但仍然执行约束来限制生成的尺寸值。在这种情况下，你可以添加一个相应的属性：

```
app：layout_constrainedWidth =”真|假”
app：layout_constrainedHeight =”真|假”
```

 **MATCH_CONSTRAINT尺寸(也就是0dp)（在1.1中添加）**

设置为MATCH_CONSTRAINT时，默认是大小是占用所有可用空间。有几个额外的修饰符可用：

```
layout_constraintWidth_min和layout_constraintHeight_min：将设置此维度的最小尺寸
layout_constraintWidth_max和layout_constraintHeight_max：将设置此维度的最大尺寸
layout_constraintWidth_percent和layout_constraintHeight_percent：将设置此维度的大小为父级的百分比
```

 ### 百分比尺寸（Percent Dimensions）

说到Percent Dimensions就不得不说ConstraintLayout中的0dp问题，当控件设置为0dp的时候（0dp的称呼又叫match_constraint），默认的行为是撑开（spread），占满可用空间，但是这个行为是可以用layout_constraintWidth_default 属性来设置的。在 ConstraintLayout 1.0.x中，这个属性还可以把它设置为wrap。而到了1.1.x，它又有了一个新的值：percent，允许我们设置控件占据可用空间的百分比。

> （注意：这在1.1-beta1和1.1-beta2中layout_constraintWidth_default是必须的，但是如果percent属性被定义,则在以下版本中不需要，然后将layout_constraintWidth_percent或layout_constraintHeight_percent属性设置为介于0和1之间的值）

下面的TextView控件将占据剩余宽度的50%和剩余高度的50%:

```
  <TextView
    android:id="@+id/textView6"
    android:layout_width="0dp"
    android:layout_height="0dp"
    
    app:layout_constraintHeight_default="percent"
    app:layout_constraintHeight_percent="0.5"
    
    app:layout_constraintWidth_default="percent"
    app:layout_constraintWidth_percent="0.5" />
   
```

### 宽高比（Ratio）

您还可以控制控件的height或者width这二个值，让其中一个值与另外一个值的成特定的比例。为此，需要至少将一个值设置为0dp（即，MATCH_CONSTRAINT），并将属性layout_constraintDimensionRatio设置为给定比率。例如：

```
<Button android:layout_width="wrap_content"
   android:layout_height="0dp"
   app:layout_constraintDimensionRatio="1:1" />
```

这样这个按钮的宽和高是一样大小的。

**Ratio可以设置为：**

- 浮点值，表示宽度和高度之间的比率
- “宽度：高度”形式的比率

**如果两个维都设置为MATCH_CONSTRAINT（0dp），则也可以使用比率：** 在这种情况下，系统设置满足所有约束条件的最大尺寸并保持指定的宽高比。

**为了约束一个特定的边，可以根据另一个边的大小来限定宽度或高度：** 可以通过在比率前面添加字母W（用于限制宽度）或H（用于限制高度），用逗号分隔来指示哪一边应该受到约束：

```
<Button android:layout_width="0dp"
   android:layout_height="0dp"
   app:layout_constraintDimensionRatio="H,16:9"
   app:layout_constraintBottom_toBottomOf="parent"
   app:layout_constraintTop_toTopOf="parent"/>
```

将按照16：9的比例设置按钮的高度，而按钮的宽度将匹配父布局的约束。

 ### 链（Chains）

链在单个轴（水平或垂直）中提供类似组的行为。

- **创建一个链:** 如果一组小部件通过双向连接链接在一起，则认为它们是一个链,如下图所示，是一个具有二个控件的最小的链：

  ![png](https://github.com/musejianglan/Wiki_Note/blob/master/img/chain_1.png)

- **链头:** 链由在链的第一个元素（链的“头”）上设置的属性控制： 

  ![png](https://github.com/musejianglan/Wiki_Note/blob/master/img/chain_2.png)

  （头是水平链最左边的部件，也是垂直链最顶端的部件。） 

- **链样式:** 在链的第一个元素上设置属性`layout_constraintHorizontal_chainStyle`或`layout_constraintVertical_chainStyle`时，链的行为将根据指定的样式进行更改（默认为CHAIN_SPREAD）。

  ![png](https://github.com/musejianglan/Wiki_Note/blob/master/img/chain_3.png)

  ```
  <?xml version="1.0" encoding="utf-8"?>
  <android.support.constraint.ConstraintLayout
      xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:app="http://schemas.android.com/apk/res-auto"
      xmlns:tools="http://schemas.android.com/tools"
      android:layout_width="match_parent"
      android:layout_height="match_parent">
      
  
      <TextView
          android:id="@+id/textView2"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="AAAA"
          app:layout_constraintHorizontal_chainStyle="spread"
          app:layout_constraintBottom_toBottomOf="parent"
          app:layout_constraintStart_toStartOf="parent"
          app:layout_constraintEnd_toStartOf="@id/textView3"
          />
  
      <TextView
          android:id="@+id/textView3"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="BBBB"
          app:layout_constraintEnd_toStartOf="@id/textView4"
          app:layout_constraintBottom_toBottomOf="parent"
          app:layout_constraintStart_toEndOf="@+id/textView2" />
  
      <TextView
          android:id="@+id/textView4"
          android:layout_width="wrap_content"
          android:layout_height="wrap_content"
          android:text="CCCC"
          app:layout_constraintBottom_toBottomOf="parent"
          app:layout_constraintEnd_toEndOf="parent"
          app:layout_constraintStart_toEndOf="@+id/textView3" />
  </android.support.constraint.ConstraintLayout>
  
  ```

  

### 屏障 (Barrier)

Barrier是一个虚拟的辅助控件，它可以阻止一个或者多个控件越过自己，就像一个屏障一样。当某个控件要越过自己的时候，Barrier会自动移动，避免自己被覆盖。 Barrier 是一个虚拟视图，类似于 Guideline，用来约束对象。Barrier 和 Guideline 的区别在于它是由多个 view 的大小决定的。在这个例子中，我们不知道 textView1 和 textView2 哪个长些，因此我们可以 基于这两个 view 的宽度创建一个Barrier。我们可以让 textView3 约束在 Barrier 后面。 

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout 
  xmlns:android="http://schemas.android.com/apk/res/android"
  xmlns:app="http://schemas.android.com/apk/res-auto"
  android:layout_width="match_parent"
  android:layout_height="match_parent">
 
  <TextView
    android:id="@+id/textView1"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginStart="16dp"
    android:layout_marginTop="16dp"
    android:text="@string/warehouse"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent" />
 
  <TextView
    android:id="@+id/textView2"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_marginStart="16dp"
    android:layout_marginTop="8dp"
    android:text="@string/hospital"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toBottomOf="@+id/textView1" />
 
  <android.support.constraint.Barrier
    android:id="@+id/barrier7"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    app:barrierDirection="end"
    app:constraint_referenced_ids="textView2,textView1" />
 
  <TextView
    android:id="@+id/textView3"
    android:layout_width="0dp"
    android:layout_height="wrap_content"
    android:layout_marginStart="8dp"
    android:text="@string/lorem_ipsum"
    app:layout_constraintStart_toEndOf="@+id/barrier7"
    app:layout_constraintTop_toTopOf="parent" />
 
</android.support.constraint.ConstraintLayout>

Barrier特别的地方就在于Barrier元素自身。app:barrierDirection 属性决定 Barrier 的方向 － 这里把它放在被引用view的后面。被引用的view 是布局中的view的id列表，用逗号隔开。
```

### 组（Group）

Group帮助你对一组控件进行设置。最常见的情况是控制一组控件的visibility。你只需把控件的id添加到Group，就能同时对里面的所有控件进行操作。

```xml
<android.support.constraint.ConstraintLayout ...>
  <TextView
    android:id=”@+id/text1" ... />
  <TextView
    android:id=”@+id/text2" ... />
  <android.support.constraint.Group
    android:id=”@+id/group”
    ...
    app:constraint_referenced_ids=”text1,text2" />
</android.support.constraint.ConstraintLayout>
```

此时如果我们调用`group.setVisibility(View.GONE);`那么text1 和 text2 都将不可见。

 ### Guideline

ConstraintLayout的辅助对象的实用程序类。Guideline不会显示在设备上（它们被标记为View.GONE），仅用于布局。他们只能在ConstraintLayout中工作。

> 指引可以是水平的也可以是垂直的： 
>
> 垂直指南的宽度为零，它们的ConstraintLayout父项的高度为零 
>
> 水平指南的高度为零，其ConstraintLayout父项的宽度为零 **定位准则有三种不同的方式：**

- 指定布局左侧或顶部的固定距离（layout_constraintGuide_begin）
- 从布局的右侧或底部指定固定距离（layout_constraintGuide_end）
- 指定布局的宽度或高度的百分比（layout_constraintGuide_percent）

> 相应的代码为setGuidelineBegin（int，int），setGuidelineEnd（int，int）和setGuidelinePercent（int，float）函数。

然后控件就可以被Guideline来约束。（换句话就是说弄了一个隐藏的View，来约束我们的控件，我们的控件相对的就更容易进行位置定位）。

### Placeholder

Placeholder顾名思义，就是用来一个占位的东西，它可以把自己的内容设置为ConstraintLayout内的其它view。因此它用来写布局的模版，也可以用来动态修改UI的内容。 

 [**New features in ConstraintLayout 1.1.x**](https://link.juejin.im/?target=http%3A%2F%2Fandroidkt.com%2Fconstraintlayout%2F) 

 

 

 

 

 

 

 

   

   