---
layout: post
keywords: blog
description: blog
title: Android 自定义View
categories: api
tags: Android 自定义 View
---

### 背景

自定义的View一般有全新自定义、组合控件两种。所以先要明确自己想要实现的效果，然后再继承类，最后复写其中的方法。

>提高代码的复用性，一处定义多处使用。

下面是自定义的标题栏，左边是返回键，中间是标题栏，右边是前进键

### 代码

* 1.编写attr.xml文件

{% highligth java %}
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <declare-styleable name="TopBar">
        <attr name="titleText" format="string" />
        <attr name="titleTextSize" format="dimension" />
        <attr name="titleColor" format="color" />

        <attr name="leftTextColor" format="color" />
        <attr name="leftBackground" format="color|reference" />
        <attr name="leftText" format="string" />

        <attr name="rightTextColor" format="color" />
        <attr name="rightBackground" format="color|reference" />
        <attr name="rightText" format="string" />

    </declare-styleable>
</resources>
{% endhighlight %}


* 2.得到view的属性值

{% highlight java %}
public class TopBar extends RelativeLayout {
....
 public TopBar(Context context, AttributeSet attrs) {
        super(context, attrs);
//		用于检索从这个结构对应于给定的属性位置到obtainStyledAttributes中的值。
        TypedArray typedArray = context.obtainStyledAttributes(attrs, R.styleable.TopBar);

        leftTextColor = typedArray.getColor(R.styleable.TopBar_leftTextColor, 0);
        leftBackground = typedArray.getDrawable(R.styleable.TopBar_leftBackground);

//		在执行完之后，一定要确保调用  recycle()函数 
        leftText = typedArray.getString(R.styleable.TopBar_leftText);
 		typedArray.recycle();

}
{% endhighlight %}

* 3.设置点击监听

{% highlight java %}
//		写一个接口
public interface TopBarClickListener {
//		左边按钮
        public void leftClick();

        public void rightClick();
    }


    leftButton.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                listener.leftClick();
            }
        });
        rightButton.setOnClickListener(new OnClickListener() {
            @Override
            public void onClick(View v) {
                listener.rightClick();
            }
        });

//	用于给外部提供的方法
    public void setOnTopBarClickListener(TopBarClickListener listener) {
        this.listener = listener;
    }
{% endhighlight %}


### 总结

以上是自定义标题栏的个别部分
