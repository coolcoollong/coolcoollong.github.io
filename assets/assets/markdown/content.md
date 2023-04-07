### 1.Stack简介:

> 可以容纳多个组件，以叠加的方式摆放子组件，后者居上。拥有**Alignment**属性，可以与**Positioned**组件联合使用，精准并有效摆放。同**Android**端**FramLayout**布局相似。

| 属性 | 作用 |
| --- | --- |
| alignment | 子组件摆放的位置 |
| clipBehavior | 剪辑小部件的内容 |

+   使用场景：

> 比如开发中需要用户头像上面添加一个特殊标识，就需要是用到堆叠布局；

![在这里插入图片描述](https://img-blog.csdnimg.cn/a0ad6e56ff774911b8ca0c78b5767d16.png)

### 创建一个堆叠布局

```java

class CustomStack extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    var yellowBox = Container(
      color: Colors.yellow,
      height: 100,
      width: 100,
    );

    var redBox = Container(
      color: Colors.red,
      height: 90,
      width: 90,
    );

    var greenBox = Container(
      color: Colors.green,
      height: 80,
      width: 80,
    );

    return Container(
      width: 200,
      height: 120,
      color: Colors.grey.withAlpha(33),
      child: Stack(
        textDirection: TextDirection.rtl,
        fit: StackFit.loose,
        alignment: Alignment.topRight,
        children: <Widget>[yellowBox, redBox, greenBox],
      ),
    );
  }
}

```

![在这里插入图片描述](assets/images/banner.jpg)

### 属性Alignment.center

![在这里插入图片描述](assets/images/img.png)  

### 属性Alignment.bottomLeft

![在这里插入图片描述](https://img-blog.csdnimg.cn/407db4ad7e6d4800b1451d8d5c794f75.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5oCA5ZCb,size_16,color_FFFFFF,t_70,g_se,x_16)  

### 2.组件Positioned

> 精准堆叠布局内部，子组件的位置与排列；

| 属性 | 作用 |
| --- | --- |
| left | 向左距离 |
| top | 向上距离 |
| right | 向右距离 |
| bottom | 向下距离 |

```java
Stack(
        textDirection: TextDirection.rtl,
        fit: StackFit.loose,
        alignment: Alignment.bottomLeft,
        children: <Widget>[
          yellowBox,
          redBox,
          Positioned(
            bottom: 10,
            right: -30,
            child: greenBox,
          )
        ],
      )
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/52c28c1689784e2c9592a4f3a764609c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5oCA5ZCb,size_16,color_FFFFFF,t_70,g_se,x_16)

> 可以看到绿色组件有一部分被裁剪调了，是因为没有使用**clipBehavior**属性，接下来我们来看**Clip.none**属性效果

### 属性clipBehavior: Clip.none

```java
Stack(
        textDirection: TextDirection.rtl,
        fit: StackFit.loose,
        alignment: Alignment.bottomLeft,
        clipBehavior: Clip.none,
        children: <Widget>[
          yellowBox,
          redBox,
          Positioned(
            bottom: 10,
            right: -30,
            child: greenBox,
          )
        ],
      ),
```

![](https://img-blog.csdnimg.cn/a84cd8cfe9e04e599b27dcbc28991191.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5oCA5ZCb,size_15,color_FFFFFF,t_70,g_se,x_16)

> 加上该属性之后我们可以看到，绿色组件超出的部分也显示出来了。该属性的意义也就一目了然。

### 3.组件Align

> 精准控制子组件的位置，同**Positioned**相似。

**创建一个带Align组件的样式**

```java
Stack(
        textDirection: TextDirection.rtl,
        fit: StackFit.loose,
        alignment: Alignment.bottomLeft,
        clipBehavior: Clip.none,
        children: <Widget>[
          Align(
            alignment: const Alignment(0, 0),
            child: redBox,
          ),
        ],
      )
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/fe54fb8b9c1c44f2bf20f3231ac41081.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5oCA5ZCb,size_16,color_FFFFFF,t_70,g_se,x_16)

> 可以看到该布局显示再正中间，Alignment(0, 0) 该属性分为 x 轴跟 y轴，范围值都是 \-1到 1 之间；

**看Alignment(0, 1)**  
![在这里插入图片描述](https://img-blog.csdnimg.cn/aff1515649b9408daf2b1561fdbb93e0.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5oCA5ZCb,size_16,color_FFFFFF,t_70,g_se,x_16)

> 可以看到当y等于1时，红色组件排列再最底部；

**看 Alignment(-0.5, -0.5)**  
![在这里插入图片描述](https://img-blog.csdnimg.cn/d128a32247a345ae83d4251b427a4ac2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5oCA5ZCb,size_16,color_FFFFFF,t_70,g_se,x_16)

> 当x等于 **\-0.5** 时，很明显组件位于横轴-1到0的中间；  
> 当y等于 **\-0.5** 时，很明显组件位于主轴-1到0的中间；  
> 总结x值的大小是根据横轴排列，y值的大小是根据主轴排列；

**属性 Alignment(1, 4)**  
![在这里插入图片描述](https://img-blog.csdnimg.cn/b6222d208fda49dbb41d00c435f948b1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5oCA5ZCb,size_16,color_FFFFFF,t_70,g_se,x_16)

> 当x与y大于1时，子组件并没有被裁剪。说明使用**Align**属性并不受**clipBehavior: Clip.none**影响；