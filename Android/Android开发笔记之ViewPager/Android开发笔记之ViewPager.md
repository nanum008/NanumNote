# Android开发笔记之ViewPager

# 一、简单使用



## 二、ViewPager适配器

### 常用方法摘要

```java
@Override
public int getCount() {
    return Integer.MAX_VALUE;
}
```

返回创建view的个数；





```java
 @Override
 public boolean isViewFromObject(@NonNull View view, @NonNull Object object) {
        //过滤和缓存的作用
        return view == object;
 }
```





```java
@Override
public void destroyItem(@NonNull ViewGroup container, int position, @NonNull Object object) {
    container.removeView((View) object);
}
```

当下一个页面创建时需要销毁上一个页面的view，防止内存溢出；



```java
@NonNull
@Override
public Object instantiateItem(@NonNull ViewGroup container, int position) {
        ImageView imageView = new ImageView(context);
        imageView.setImageResource(images.get(position%images.size()));
        container.addView(imageView);
        container.setBackgroundColor(Color.rgb(12,43,99));
        return imageView;
    }
}
```

创建页面时调用此方法；

参数container就是viewpager的view，我们在此方法里创建的view就是container的子view；



## 三、ViewPager监听器
