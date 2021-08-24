# Android自定义控件之视图篇

> 尽管Google为我们提供了大量的UI控件，但是在当经这个追求个性的时代，Google当我们的UI组件已经不能满足我们的需求。
>
> 所以我们需要根据我们的业务需求去定制符合自己需求的UI控件。

我们通常自定义一个View的派生类来实现我们的特殊业务需求。在Android中View类是所有UI控件的基类，像我们日常所用到的TextView、Button、LinearLayout等都是View的派生类。自定义的View需要我们去定义构造函数，一共四个。

### 构造函数

```java
public class CustomView extends View{
    public CustomView(Context context){}
    public CustomView(Context context,AttributeSet attrs){}
    public CustomView(Context context,AttributeSet attrs,int defStyleAttr){}
}
```

```java
public CustomView(Context context){}
```

我们new自定义的View时会调用第一个构造函数。参数就一个上下文(Context)，没什么好说的。



```java
public CustomView(Context context,AttributeSet attrs){}
```

当我们在xml文件中定义我们自定义的View时会调用第二个构造函数。我们可以在第二个参数(AttributeSet)中获取到我们自定义的属性。

**自定义属性**

```java
TypedArry typedArry =  context.obtainStyledAttributes(attrs, R.styleable.MyTextView);
//回收TypedArry的原因：
//TypedArry是高频使用的对象，为了提升效率，系统在堆内存里预先准备了几个TypedArry对象，当我们需要的时候就在堆内存里取，不需要的
//时就调用Recycle()方法将其回收，放回堆内存以便复用，这样可以避免频繁的new TypedArry对象，避免消耗内存。
typedArry.recycle();
```

onMaesure()方法

public static class MeasureSpec:

public static String toString(int measureSpec) 

作用：返回包含measureSpec信息的一个字符串，格式为："MeasureSpec: MODE SIZE"

step1：调用getMode(int measureSpec)和getSize(int measureSpec)方法得到mode和size的大小值。

step2：mode的大小值与UNSPECIFIED、EXACTLY、AT_MOST三者之一匹配则"MeasureSpec: MODE SIZE"中的MODE为对应的模式名称，否则mode大小值，。

step3：字符串拼接返回。

measure specification based on the supplied size and mode.

### 安桌自定义view三部曲

1.  onMeasure()测量
2.  onLayout()布局
3.  onDrow()绘制



### 控件宽高获取

PS:以下方式获取到的尺寸大小均是以像素(px)为单位。

**一：获取视图尺寸大小**

- int getLeft()

  获取视图左边到父视图左边的距离

- int getTop()

  获取视图顶边到父视图顶边的距离

- int  getRight()

  获取视图右边到父视图左边的距离

- int  geBottom()

  获取视图底边到父视图顶边的距离

  由以上方法可以得出：视图高度 = getBottom() - getTop()、视图宽度 = getRight() - getLeft() 

**二：获取测量阶段视图宽高尺寸**

​		int getMeasureWidth()

​		int getMeasureHeight()

​		获取当前视图在**测量阶段**的宽和高。即自定义View时在”setMeasuredDimension(int width,int height)“方法传入的参数。

**三：获取布局阶段视图宽高尺寸**

​		int getWidth()

​		int getHeight()

​		获取当前视图在**布局阶段**的宽和高。 即自定义View时在"layout()"f方法传入的参数。

