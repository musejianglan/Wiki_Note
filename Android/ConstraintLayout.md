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

![ConstraintLayout_1.png.png](https://github.com/musejianglan/Wiki_Note/blob/master/img/ConstraintLayout_1.png.png)