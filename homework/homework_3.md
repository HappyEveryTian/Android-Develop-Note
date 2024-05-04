# 1. 实现一个列表，要求具有点击事件，item样式需包含文字图片

1. 在activity_main.xml中引入RecycleView

```
    <androidx.recyclerview.widget.RecyclerView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:id="@+id/demo_recycleView"/>
```
2. 创建JavaBean存储数据元素，此处创建的是GameBean,两个参数分别设置游戏图片和游戏名称

```
public class GameBean {
    private int Game_Icon_Id;
    private String Game_Name;
    public GameBean(int game_Icon_Id,String game_Name){
        this.Game_Icon_Id = game_Icon_Id;
        this.Game_Name = game_Name;
    }
    ......
}
```

3. 编写RecycleView适配器GameRecycleAdapter

```
public class GameRecycleAdapter extends RecyclerView.Adapter<GameRecycleAdapter.ViewHolder> {
    private List<GameBean> mDataList;
    public GameRecycleAdapter(List<GameBean> mDataList) {
        this.mDataList = mDataList;
    }
    public static class ViewHolder extends RecyclerView.ViewHolder {
        ImageView mGameIcon;
        TextView mGameName;
        public ViewHolder(@NonNull View itemView) {
            super(itemView);
            mGameIcon = itemView.findViewById(R.id.game_icon);
            mGameName = itemView.findViewById(R.id.game_name);
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
    }
    ......
}
```

4. 在MainActivity中设置RecycleView

```
    private RecyclerView recyclerView;

    private GameRecycleAdapter adapter;

    private LayoutManager layoutManager;

    ......

    recyclerView = findViewById(R.id.demo_recycleView);
    
    recyclerView.setHasFixedSize(true);

    layoutManager = new LinearLayoutManager(this);

    recyclerView.setLayoutManager(layoutManager);

    List<GameBean> mylist = new ArrayList<>();
        //添加数据
        for(int i = 1;i<=20;i++) {
            GameBean gameBean = new GameBean(R.drawable.game,"英雄联盟");
            mylist.add(gameBean);
        }
    
    adapter = new GameRecycleAdapter(mylist);
    recyclerView.setAdapter(adapter);
```

5. 设置点击事件

```
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
```
### 截图
![start](/homework/asset/homeworkImage_3/start.png)

# 2. 实现增加删除列表项功能

1. 在activity_main.xml中引入增加、删除按钮

```
    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/add_btn"
        android:text="增加"/>

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/remove_btn"
        android:text="删除"/>
```

2. 为增加、删除按钮增加点击事件实现增加、删除列表项

```
    addItem.setOnClickListener((view) -> {
        if(editText.getText().length()==0) return;
        int position = Integer.parseInt(editText.getText().toString());
        mylist.add(position,addGameBean);
        adapter.notifyItemInserted(position);
        adapter.notifyItemRangeChanged(position,mylist.size());
        text.setText("add Item: " + position);
        Toast toast = new Toast(getApplicationContext());
        toast.setDuration(Toast.LENGTH_SHORT);
        toast.setView(layout);
        toast.show();
    });
    removeItem.setOnClickListener((view) -> {
        if(editText.getText().length()==0) return;
        int position = Integer.parseInt(editText.getText().toString());
        if(position >= mylist.size()) return;
        mylist.remove(position);
        adapter.notifyItemRemoved(position);
        adapter.notifyItemRangeChanged(position,mylist.size());
        text.setText("remove Item: " + position);
        Toast toast = new Toast(getApplicationContext());
        toast.setDuration(Toast.LENGTH_SHORT);
        toast.setView(layout);
        toast.show();
    });
```

### 截图

1. 在指定的索引处增加列表项功能
![add](/homework/asset/homeworkImage_3/add.png)

2. 在指定的所引出删除列表项功能(如超出索引，则无响应，待优化)
![remove](/homework/asset/homeworkImage_3/remove.png)
