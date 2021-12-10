# ViewPager详解

## 一、ViewPager常用方法

- void setAdapter( @Nullable PagerAdapter adapter )

  作用：为ViewPger绑定适配器；

-  void setCurrentItem( int item ) 

  作用：设置当前展示的是哪一页(page)，常见的Banner轮播图自动翻页的实现原理就是利用该方法；

- void setPageMargin( int marginPixels )

  作用：设置page之间的间距；

- void setOffscreenPageLimit( int limit )

  作用：设置偏移出屏幕的page数量，也就是预加载多少个page；假设`limit` 是2，那么ViewPager加载的page数就是：当前显示的page(1)+预加载的page(2) = 3；

- void setPageTransformer( boolean reverseDrawingOrder , @Nullable PageTransformer transformer )

     作用：为ViewPager绑定PageTransFormer，`PageTransFormer`的作用是控制page切换时的动画效果，参数`reverseDrawingOrder `的作用是： ；

- void addOnPageChangeListener( @NonNull OnPageChangeListener listener )

     作用：为ViewPager绑定监听器，处理用户点击、滑动等事件的响应；





## 二、PageAdapter

> `PageAdapter`用于处理`ViewPager`创建的page个数、每一个page的视图(view)等工作；

```java
```



## 三、OnPageChangeListener

> `OnPageChangeListener`是`ViewPager`的一个内部类，用于处理用户对`ViewPager`产生的点击、滑动等事件的响应；
>
> 

```java

ViewPager vp = new ViewPager();

 
```



## 四、PageTransformer

> `PagerTransFormer`用于控制当用户滑动ViewPager时，page切换时的动画效果；

```java
```

