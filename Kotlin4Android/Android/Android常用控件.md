## findViewById

* 常规用法
xml  

```
	<TextView
        android:id="@+id/textview"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        android:text="TextView"
        />

```

activity

```
	var text:TextView? = null;
	
  	text = findViewById(R.id.textview)
```

* 使用了apply plugin: 'kotlin-android-extensions'扩展插件

> apply plugin: 'kotlin-android-extensions'

在activity中导入
`import kotlinx.android.synthetic.main.activity_main.*`

activity_main是layout的名称；代码中可以省略findViewById；直接通过控件id使用该控件

```
import kotlinx.android.synthetic.main.activity_main.*

class MyActivity : Activity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        
        // Instead of findViewById<TextView>(R.id.textView)
        textView.setText("Hello, world!")
    }
}
```
textView 是对 Activity 的一项扩展属性，与在 activity_main.xml 中的声明具有同样类型(id) (so it is a TextView)。

* 导入合成属性

仅需要一行即可非常方便导入指定布局文件中所有控件属性：

`import kotlinx.android.synthetic.main.＜布局＞.*`

若需要调用 View 的合成属性，同时还应该导入 
`kotlinx.android.synthetic.main.activity_main.view.*`

## 基本属性设置，以TextView为例

```
		//设置文字
        text?.setText(string)
        //设置字体
        text?.textSize = 25f
        //设置字体颜色
        text?.setTextColor(Color.RED)
        //字体样式
        text?.typeface = Typeface.SANS_SERIF
        //
        text?.gravity = Gravity.CENTER
        //
        text?.ellipsize = TextUtils.TruncateAt.MIDDLE
        //
        text?.setCompoundDrawablesWithIntrinsicBounds(R.mipmap.ic_launcher_round,0,0,0)
        //
```

## 点击事件

* 第一种
	button?.setOnClickListener(View.OnClickListener {
            // todo
        })

* 第二种方式
xml

```
<Button
        android:text="rxxxxx"
        android:onClick="rxxxxx"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>
```

activity

```

	fun rxxxxx(view:View):Unit{

        // todo

    }
```

和Java一样，在xml中设置onClick属性，activity中添加对应的方法；目前还无法自动生成，只能手写该方法  

## 适配器Adapter

#### ListView

```
class ListAdapter(var list:MutableList<Forcecast>?,var context:Context) : BaseAdapter() {
    override fun getView(position: Int,convertView: View?, parent: ViewGroup?): View? {

        var viewholder:ViewHolder2
        var v:View//必须使用新的变量，无法直接使用convertView
        if (convertView == null) {
            viewholder = ViewHolder2()
            v = LayoutInflater.from(context).inflate(R.layout.item_text,null)

            viewholder.textview = v.findViewById(R.id.text)
            v.tag = viewholder

        } else {

            v = convertView
            viewholder = v.tag as ViewHolder2
        }
        val forcecast = list?.get(position)
        viewholder.textview?.setText("${forcecast?.date?.time} + ${forcecast?.temperature} + ${forcecast?.details}")
        return v
    }

    override fun getItem(position: Int): Forcecast? {
        return list?.get(position)
    }

    override fun getItemId(position: Int): Long {
        return position.toLong()
    }

    override fun getCount(): Int {
        return list?.size ?: 0
    }

    class ViewHolder2{


        var textview:TextView? = null
    }
}
```


#### RecyclerView

```
class ForecastListAdapter(val items:List<String>) :RecyclerView.Adapter<ForecastListAdapter.ViewHolder>() {
    override fun getItemCount(): Int {
        return items.size
    }

    override fun onBindViewHolder(holder: ViewHolder?, position: Int) {
        holder?.textview?.text = items[position]
    }

    override fun onCreateViewHolder(parent: ViewGroup?, viewType: Int): ViewHolder {
        var view:View = LayoutInflater.from(parent?.context).inflate(R.layout.item_text,parent,false)
        return ViewHolder(view)
    }


    class ViewHolder(val view: View) : RecyclerView.ViewHolder(view) {
        var textview :TextView? = null;

        init {
            textview = view.findViewById(R.id.text)
            //还不会使用扩展插件，所以必须使用findviewById
        }

    }
}
```






