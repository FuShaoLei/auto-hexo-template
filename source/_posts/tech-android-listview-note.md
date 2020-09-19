---
title: Listview学习
date: 2020-06-24 08:37:32
categories: Android
---
> Listview是入门android的重点，当初浅尝辄止，不是很理解原理，如今重新来过，希望有不一样的感悟

## 简介
### AdapterView
容器控件，其整体效果由每一个子元素内容决定，子元素的形式由Adapter决定。
常见子类：
- ListView 垂直列表
- GridView 网格列表
- Spinner 下拉列表

待显示的数据如何传递给AdapterView中的Item？
- 准备数据 （数据和item是匹配的）
- 借助Adapter来实现数据与View之间的数据传递。

### Adapter
将数据显示到视图上，数据和视图之间交互的中介。

### 图解
![](https://cdn.jsdelivr.net/gh/fushaolei/img/20200624094442.png)

### 作用
- 将数据和视图分开了，数据改变时，不需要修改视图组件，只需更新Adapter
- 对于同一组数据，可以显示为不同的视图形式

### 常用Adapter
- ArrayAdapter：最简单的适配器，数据源为文本字符串数组。
- SimpleAdapter：简单适配器，数据源结构比较复杂，一般为List<Map>类型对象。
- SimpleCursorAdapter：游标适配器，数据源一般为数据库中（SQLite）的数据。
- **自定义适配器**：更灵活的适配器，数据源不定（由用户自行指定），需要继承BaseAdapter抽象类。

> 实际项目中，自定义适配器用的比较多


## 基本流程

1. 准备数据源 
2. 准备AdapterView每一个子项（item）的视图布局。
3. 创建Adapter（**连接数据源和视图布局**）。
4. 为指定AdapterView视图组件绑定适配器。
5. 为AdapterView绑定（item）事件监听器。

## 自定义Adapter

### 基础样式
```java
/**
 * 继承BaseAdapter后需要完成四个方法
 * 1. getCount() 获得数据的条数
 * 2. getItem(int position) 获取每个item显示的数据对象
 * 3. getItemId(int position) 获取每个item的id的值
 * 4. getView(int position, View convertView, ViewGroup parent) 获取item的视图对象
 */
public class MyAdapter extends BaseAdapter {
    /**
     * 三个必要的东西：
     * 1.环境上下文
     * 2.数据源 类型
     * 3. item布局文件
     */
    private Context mContext;
    private List<Student> students = new ArrayList<>();
    private int itemLinearRes;

    public MyAdapter(Context mContext, List<Student> students, int itemLinearRes) {
        this.mContext = mContext;
        this.students = students;
        this.itemLinearRes = itemLinearRes;
    }

    @Override
    public int getCount() {//获得数据的条数
        if (null != students) {
            return students.size();
        }
        return 0;
    }

    @Override
    public Object getItem(int position) {//获取每个item显示的数据对象
        if (null != students) {
            return students.get(position);
        }
        return null;
    }

    @Override
    public long getItemId(int position) {//获取每个item的id的值
        return position;
    }

    @Override
    //获取item的视图对象
    /**
     * 1.position 表示条数
     * 2.convertView每一个item的视图对象（通过手动的加载布局文件来创建出视图对象）
     * 3.parent ListView本身
     */
    public View getView(int position, View convertView, ViewGroup parent) {
        //1. 加载item的布局文件来创建出item的视图对象
        //这一步其实和setContentView一样
        // LayoutInflater布局填充器
        if (convertView == null) {//当converView为空时才加载
            LayoutInflater inflater = LayoutInflater.from(mContext);//创建布局填充其
            convertView = inflater.inflate(itemLinearRes, null);//可加载布局文件
        }
//  上面两行可以简化写成这样 convertView=LayoutInflater.from(mContext).inflate(itemLinearRes,null);

        //2. 获取item控件的引用
        ImageView img = convertView.findViewById(R.id.img_item);
        TextView name = convertView.findViewById(R.id.tv_name_item);
        TextView no = convertView.findViewById(R.id.tv_name_no);

        //3.设置控件内容
        img.setImageResource(students.get(position).getPhotoId());
        name.setText(students.get(position).getName());
        no.setText(students.get(position).getStuiNo());

        return convertView;//return视图
    }
}

```

### 改良一：重用
1. 在`MyAdapter`中定义一个`class`在里边写item里的控件

```java
    public static class ViewHolder{//通常取名为ViewHolder
        ImageView vImg;
        TextView vName;
        TextView vNum;
    }
```
然后部分东西就可以复用啦，好像也没有上什么改良的东西。。。

```java
    /**
     * 改良过后
     */
    public View getView(int position, View convertView, ViewGroup parent) {
        ViewHolder viewHolder;
        if (null==convertView){
            convertView=LayoutInflater.from(mContext).inflate(itemLinearRes,null);
            viewHolder=new ViewHolder();
            viewHolder.vImg=convertView.findViewById(R.id.img_item);
            viewHolder.vName=convertView.findViewById(R.id.tv_name_item);
            viewHolder.vNum=convertView.findViewById(R.id.tv_name_no);
            convertView.setTag(viewHolder);//将ViewHolder存储到convertView中
        }else {
            viewHolder=(ViewHolder) convertView.getTag();
        }
        viewHolder.vImg.setImageResource(students.get(position).getPhotoId());
        viewHolder.vName.setText(students.get(position).getName());
        viewHolder.vNum.setText(students.get(position).getStuiNo());

        return convertView;//return视图
    }

```

## 构建万能的BaseAdapter 

> 这是在菜鸟教程里看到的，文章指路：[构建一个可复用的自定义BaseAdapter](https://www.runoob.com/w3cnote/android-tutorial-customer-baseadapter.html)

```java
import android.content.Context;
import android.util.SparseArray;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.ImageView;
import android.widget.TextView;

import java.util.ArrayList;

public abstract class MyAdapter<T> extends BaseAdapter {

    private ArrayList<T> mData;
    private int mLayoutRes;           //布局id
    
    /**
     * @param mData 数据
     * @param mLayoutRes item的布局文件
     */
    public MyAdapter(ArrayList<T> mData, int mLayoutRes) {
        this.mData = mData;
        this.mLayoutRes = mLayoutRes;
    }

    @Override
    public int getCount() {
        return mData != null ? mData.size() : 0;
    }

    @Override
    public T getItem(int position) {
        return mData.get(position);
    }

    @Override
    public long getItemId(int position) {
        return position;
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        ViewHolder holder = ViewHolder.bind(parent.getContext(), convertView, parent, mLayoutRes
                , position);
        bindView(holder, getItem(position));
        return holder.getItemView();
    }

    public abstract void bindView(ViewHolder holder, T obj);

    //添加一个元素
    public void add(T data) {
        if (mData == null) {
            mData = new ArrayList<>();
        }
        mData.add(data);
        notifyDataSetChanged();
    }

    //往特定位置，添加一个元素
    public void add(int position, T data) {
        if (mData == null) {
            mData = new ArrayList<>();
        }
        mData.add(position, data);
        notifyDataSetChanged();
    }

    public void remove(T data) {
        if (mData != null) {
            mData.remove(data);
        }
        notifyDataSetChanged();
    }

    public void remove(int position) {
        if (mData != null) {
            mData.remove(position);
        }
        notifyDataSetChanged();
    }

    public void clear() {
        if (mData != null) {
            mData.clear();
        }
        notifyDataSetChanged();
    }


    public static class ViewHolder {

        private SparseArray<View> mViews;   //存储ListView 的 item中的View
        private View item;                  //存放convertView
        private int position;               //游标
        private Context context;            //Context上下文

        //构造方法，完成相关初始化
        private ViewHolder(Context context, ViewGroup parent, int layoutRes) {
            mViews = new SparseArray<>();
            this.context = context;
            View convertView = LayoutInflater.from(context).inflate(layoutRes, parent, false);
            convertView.setTag(this);
            item = convertView;
        }

        //绑定ViewHolder与item
        public static ViewHolder bind(Context context, View convertView, ViewGroup parent,
                                      int layoutRes, int position) {
            ViewHolder holder;
            if (convertView == null) {
                holder = new ViewHolder(context, parent, layoutRes);
            } else {
                holder = (ViewHolder) convertView.getTag();
                holder.item = convertView;
            }
            holder.position = position;
            return holder;
        }

        @SuppressWarnings("unchecked")
        public <T extends View> T getView(int id) {
            T t = (T) mViews.get(id);
            if (t == null) {
                t = (T) item.findViewById(id);
                mViews.put(id, t);
            }
            return t;
        }


        /**
         * 获取当前条目
         */
        public View getItemView() {
            return item;
        }

        /**
         * 获取条目位置
         */
        public int getItemPosition() {
            return position;
        }

        /**
         * 设置文字
         */
        public ViewHolder setText(int id, CharSequence text) {
            View view = getView(id);
            if (view instanceof TextView) {
                ((TextView) view).setText(text);
            }
            return this;
        }

        /**
         * 设置图片
         */
        public ViewHolder setImageResource(int id, int drawableRes) {
            View view = getView(id);
            if (view instanceof ImageView) {
                ((ImageView) view).setImageResource(drawableRes);
            } else {
                view.setBackgroundResource(drawableRes);
            }
            return this;
        }


        /**
         * 设置点击监听
         */
        public ViewHolder setOnClickListener(int id, View.OnClickListener listener) {
            getView(id).setOnClickListener(listener);
            return this;
        }

        /**
         * 设置可见
         */
        public ViewHolder setVisibility(int id, int visible) {
            getView(id).setVisibility(visible);
            return this;
        }

        /**
         * 设置标签
         */
        public ViewHolder setTag(int id, Object obj) {
            getView(id).setTag(obj);
            return this;
        }

        //其他方法可自行扩展

    }

}
```

使用示范
```java
        /**
         * 1.第一个参数是数据
         * 2.第二个参数是item的布局文件
         */
        myAdapter=new MyAdapter<Student>(studentArrayList,R.layout.student_item) {
            @Override
            public void bindView(ViewHolder holder, Student obj) {
                holder.setImageResource(R.id.img_item,obj.getPhotoId());
                holder.setText(R.id.tv_name_item,obj.getName());
                holder.setText(R.id.tv_name_no,obj.getStuiNo());
            }
        };
        listView.setAdapter(myAdapter);
```

> 这里没有细看 改天再看看