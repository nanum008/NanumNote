# Android自定义控件之绘图篇

## 一、Paint与Canvas

> 工欲善其事必先利其器。想要在自定义的View上画出符合我需求的内容，我们需要先了解"画画"的工具：笔(Paint)和纸(Canvas)，这两个类封装了大量的视图绘制操作，让我们可以轻松地在我们的应用中绘出优美的图形。

### 1. Paint

###### 主要函数：

- **void setColor()	**设置画笔颜色

  参数说明：

- **void setStytle()     **设置画笔样式

  参数说明：

- **void setAntiAlias(boolean aa)   **设置画笔抗锯齿

  参数说明：传入true即可开启抗锯齿效果，使视图绘制更加流畅。

- **void setStrokeWidth()   **设置画笔粗细

以上函数可以为我们设置画笔的属性，值得一提的是



### Canvas

###### 主要函数：

- viod drawLine(float startX,float startY,float endX,float endY,Paint paint)

  说明：在视图中画出一条线。前四个坐标对应直线的起始点和结束点坐标，有了这两个点的坐标，一条直线的位置和长度就可以确定了。

- 

- 

- 

- 

###### 示例：



## 二、基本几何图形绘制

## 三、路径(Path)绘制

## 四、区域(Range)绘制