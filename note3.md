# Android UI 控件

Android应用界面包含用户可查看并与之交互的所有内容。Android 提供丰富多样的预置UI组件，例如结构化布局对象和UI控件。你可以利用这些组件为你的应用构建图形界面。Android UI都是由布局和控件组成的。

## View常用属性介绍

- 像素(px): 单位：px(pixel), 1px = 1 像素点。像素是手机屏幕的最小构成单元。
- 分辨率: 手机在横向、纵向上的像素点数总和一般描述成宽 \* 高，即横向
像素点个数 \* 纵向像素点个数(如1080x1920)。单位:px(pixel)，1px=1像素点。
- 屏幕尺寸(in): 手机对角线的物理尺寸。单位:英寸(inch)，一英寸大约2.54cm。常见的尺寸有4.7寸、5寸、5.5寸、6寸。
- 屏幕像素密度(dpi): 每英寸的像素点数。例如每英寸内有160个像素点则其像素密度为160dpi。单位:dpi(dots perinch)
- 标准屏幕像素密度(mdpi):每英寸长度上有160个像素点(160dpi)即称为标准屏幕像素密度(mdpi)。

![dpi1](/image_day_3/dpi1.png)

- 密度无关像素(dp): density-independent pixel，dp或dip，与终端上的实际物理像素点无关单位:dp，可以保证在不同屏幕像素密度的设备上显示相同的效果，是安卓特有的长度单位。

- 独立比例像素(sp): scale-independentpixel，sp或sip。单位:sp，字体大小专用单位。Android开发时用此单位设置文字大小，可根据字体大小首选项进行缩放;推荐使用12sp、14sp、18sp、22sp作为字体大小，不推荐使用奇数和小数，容易造成精度丢失，12sp以下字体太小。

![dpi2](/image_day_3/dpi2.png)

![dpi3](/image_day_3/dpi3.png)

### 常用属性

![view](/image_day_3/view.png)

### Res目录介绍

- values/ 

    包含字符串、整型数和颜色等简单值的 XML文件。其他 res/ 子目录中的XML 资源文件会根据 XML 文件名定义单个资源，而values/目录中的文件可描述多个资源。对于此目录中的文件，元素的每个子元素均会定义一个资源。例如，元素会创建R.string 资源，元素会创建 R.color 资源。由于每个资源均使用自己的 XML元素进行定义，因此您可以随意命名文件，并在某个文件中放入不同的资源类型。但是，您可能需要将独特的资源类型放在不同的文件中，使其一目了然例如，对于可在此目录中创建的资源，下面给出了相应的文件名约定:

    arrays.xml:资源数组(类型数组)。

    colors.xml:颜色值。

    dimensxxml:尺寸值。

    strings.xml:字符串值。

    styles.xml:样式。

- xml/ 

    可在运行时通过调用 Resources.getXML()读取的任意 XML 文件。各种 XML配置文件(如可搜索配置)都必须保存在此处。

- font/

    带有扩展名的字体文件(如 .ttf、.otf 或 .ttc)，或包含 元素的 XML 文件。

## 常用UI部件

### 1. TextView

- android:text：设置 TextView 中显示的文本内容。
- android:textColor：设置文本的颜色。
- android:textSize：设置文本的大小。
- android:gravity：设置文本在 TextView 中的对齐方式，如左对齐、居中、右对齐等。
- android:layout_width 和 android:layout_height：设置 TextView 的宽度和高度。
- android:background：设置 TextView 的背景，可以是颜色、图片等。
- android:padding：设置文本与 TextView 边缘的内边距。
- android:fontFamily：设置字体系列，指定使用哪种字体。
- android:textStyle：设置文本样式，如正常、粗体、斜体等。
- style: 和 android:textAppearance: 为文本应用样式表。
- android:singleLine 或 android:maxLines：设置 TextView 是否单行显示，或者最大显示行数。
- android:ellipsize：设置当文本过长时的省略方式，如省略号结尾、跑马灯效果等。
- android:scrollbars：设置滚动条的显示方式，如垂直滚动条、水平滚动条等。
- android:focusableInTouchMode: 设置触摸获取焦点。
- android:drawableLeft(Right/Top/Bottom)：设置在文本的左侧、顶部、右侧、底部显示的图标。
- android:drawablePadding：设置文本与图标之间的间距。
- android:textAlignment：设置文本在 TextView 中的对齐方式，如文本居左、居中、居右等。

#### SpannableString设置富文本

![spannablestring](/image_day_3/spannablestring.png)

示例

![spannablecase](/image_day_3/spannablecase.png)

### 2. Button

在UI上生成一个按钮，可供用户单击，当用户单击按钮时，触发一个onclick事件。Button是TextView的子类，所以TextView上很多属性也可以应用到Button上!实际开发中对于Button的使用，主要对按钮的几个状态做相应的操作，比如:按钮按下的时候 用一种样式，松开又一种样式，或者按钮不可用的时候一种样式等等.

- button.setOnClickListener(): 设计点击事件
- button.setOnLongClickListener(): 设计长按事件
- button.setOnTouchListener(): 设计触摸事件 

#### StateListDrawable

StateListDrawable 是在 XML文件中定义的可绘制对象，它会根据对象状态，使用多个图像来表示同一个图形。例如，Button的状态可以是按下、聚焦或既不按下也不聚焦;而使用状态列表可以为每种状态提供不同的背景图像。

命名为 drawable button click.xml

\<item>定义在某些状态下使用的可绘制对象，状态通过其属性来描述。

### 3. RadioButton

RadioButton（单选按钮）是 Android 中的一个视图控件，用于在一组选项中进行单选操作。通常情况下，当用户需要从多个选项中选择一个时，可以使用 RadioButton。RadioButton 可以单独使用，也可以与 RadioGroup 结合使用，以便在多个 RadioButton 中实现单选效果。

- 通常情况下，我们会将多个 RadioButton 放置在一个 RadioGroup 中，以确保在同一组中只能选择一个选项。这样做可以简化单选按钮的管理，并且当一个 RadioButton 被选中时，其他 RadioButton 会自动变为未选中状态。

### 4. CheckBox

多选框（CheckBox）是 Android 中的一个常见视图控件，用于在用户可以从多个选项中选择多个选项。与单选按钮（RadioButton）类似，但 CheckBox 允许用户选择多个选项，而不是单选一个选项。

- 当用户点击 CheckBox 时，它会切换自身的选中状态。如果它之前未被选中，则会变为选中状态；如果之前已被选中，则会变为未选中状态。

### 5. ToggleButton

ToggleButton 是 Android 中的一个视图控件，允许用户切换两种状态之间的选择。它类似于一个开关按钮，用户可以点击它来切换它的状态。ToggleButton 可以用于打开/关闭、切换功能、设置选项等场景。

- ToggleButton 只有两种状态，打开和关闭。用户可以点击它来切换状态。

### 6. Switch

Switch 是 Android 中的一个视图控件，用于在用户可以切换两种状态之间的选择。它类似于一个切换按钮，用户可以通过滑动来切换它的状态。Switch 可以用于打开/关闭、切换功能等场景。

- Switch 只有两种状态，打开和关闭。用户可以通过滑动来切换状态。

### 7. EditText

EditText 是 Android 中的一个常见的文本输入控件，允许用户在应用程序中输入文本。它可以用于接受用户的文本输入，例如用户名、密码、搜索关键字等。

- 可以通过 android:inputType 属性设置 EditText 的输入类型，例如文本、数字、密码、电子邮件等。不同的输入类型会影响键盘的显示和输入行为。
- 可以通过 addTextChangedListener() 方法监听 EditText 中文本的变化，以便在文本发生变化时执行相应的操作。
- 可以使用 getText() 方法获取 EditText 中的文本内容，使用 setText() 方法设置 EditText 的文本内容。

### 8. ImageView

ImageView 是 Android 中用于显示图像的视图控件。它可以显示来自资源文件、Drawable 对象、位图对象或网络 URL 的图像。以下是一些关于 ImageView 的重要特性和用法：

- 可以通过设置 ImageView 的缩放类型（scaleType）来控制图像的缩放和裁剪方式，例如居中、拉伸、等比例缩放等。
- 可以从多种来源加载图像，包括资源文件（drawable 文件夹中的图像）、Drawable 对象、位图对象或者通过网络下载的图像。

### 9. ProgressBar

ProgressBar 是 Android 中用于显示进度的视图控件，通常用于表示某个操作的完成进度或加载进度。它可以显示一个动画或静态的进度条，用户可以通过观察进度条的变化来了解操作的进展情况。

- ProgressBar 可以显示为确定性进度（indeterminate）或不确定性进度（determinate）。确定性进度表示已知操作的完成程度，而不确定性进度表示正在进行的操作，但不知道何时会完成。

### 10. SeekBar

SeekBar 是 Android 中的一个滑动条控件，允许用户在一个范围内拖动滑块来选择值。它通常用于调整音量、亮度、进度等需要连续调整的参数。

- SeekBar 可以设置一个范围，用户只能在这个范围内选择值。
- 可以通过设置 OnSeekBarChangeListener 来监听用户选择的值的变化，并在值发生变化时执行相应的操作。

### 11. Bitmap

Bitmap 是 Android 中表示图像的类，它提供了处理和操作图像的方法。Bitmap 类可以从多种来源创建，例如资源文件、文件路径、字节数组等，也可以将其绘制到画布上或保存到文件中。

- Bitmap 类提供了一些方法来处理图像，例如缩放、旋转、裁剪、颜色滤镜等。
- 可以将 Bitmap 保存到文件中，例如 PNG、JPEG 等格式。

### 12. RecycleView

RecyclerView 是 Android 中用于显示大量数据列表的高性能控件，是 ListView 和 GridView 的增强版。它支持灵活的布局管理、数据适配、动画效果等功能，可以有效地处理大量数据并提高列表的性能。

```
// 在 XML 布局中定义 RecyclerView
<androidx.recyclerview.widget.RecyclerView
    android:id="@+id/recycler_view"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />

// 在 Activity 或 Fragment 中找到 RecyclerView
RecyclerView recyclerView = findViewById(R.id.recycler_view);

// 设置布局管理器
recyclerView.setLayoutManager(new LinearLayoutManager(this)); // 设置线性布局管理器
// recyclerView.setLayoutManager(new GridLayoutManager(this, 2)); // 设置网格布局管理器
// recyclerView.setLayoutManager(new StaggeredGridLayoutManager(2, StaggeredGridLayoutManager.VERTICAL)); // 设置瀑布流布局管理器

// 创建数据列表
List<String> dataList = new ArrayList<>();
//添加数据
dataList.add();

// 创建适配器并设置给 RecyclerView
RecyclerViewAdapter adapter = new RecyclerViewAdapter(dataList);
recyclerView.setAdapter(adapter);

// 设置点击事件监听器
adapter.setOnItemClickListener(new RecyclerViewAdapter.OnItemClickListener() {
    @Override
    public void onItemClick(View view, int position) {
        // 处理列表项点击事件
        Toast.makeText(MainActivity.this, "Clicked: " + dataList.get(position), Toast.LENGTH_SHORT).show();
    }
});
```

#### 适配器的创建

```
public class GameRecycleAdapter extends RecyclerView.Adapter<GameRecycleAdapter.ViewHolder> {
    private List<GameBean> mDataList;
    public GameRecycleAdapter(List<GameBean> mDataList) {
        this.mDataList = mDataList;
    }
    public static class ViewHolder extends RecyclerView.ViewHolder {
        ImageView mGameIcon;
        TextView mGameName;
        Button mGameButton;
        public ViewHolder(@NonNull View itemView) {
            super(itemView);
            mGameIcon = itemView.findViewById(R.id.game_icon);
            mGameName = itemView.findViewById(R.id.game_name);
            mGameButton = itemView.findViewById(R.id.game_button);
        }
    }
    @NonNull
    @Override
    public ViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext())
                .inflate(R.layout.item_layout, parent, false);
        return new ViewHolder(view);
    }
    @Override
    public void onBindViewHolder(@NonNull ViewHolder holder, int position) {
        GameBean gameBean = mDataList.get(position);
        holder.mGameIcon.setImageResource(gameBean.getGame_Icon_Id());
        holder.mGameName.setText(gameBean.getGame_Name());
        // 修改 mGameIcon 的大小
        ViewGroup.LayoutParams layoutParams = holder.mGameIcon.getLayoutParams();
        layoutParams.width = 100; // 设置宽度为 100 像素
        layoutParams.height = 100; // 设置高度为 100 像素
        holder.mGameIcon.setLayoutParams(layoutParams);
        holder.mGameButton.setOnClickListener((view) -> {
            Toast.makeText(view.getContext(),"Clicked",Toast.LENGTH_SHORT).show();
        });
    }
}

```

#### 分割线的使用

```
/ 创建分割线装饰
DividerItemDecoration decoration = new DividerItemDecoration(this, DividerItemDecoration.VERTICAL);
decoration.setDrawable(getResources().getDrawable(R.drawable.divider_line));

// 将分割线装饰添加到 RecyclerView
recyclerView.addItemDecoration(decoration);
```