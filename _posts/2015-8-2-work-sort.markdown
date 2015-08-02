---
layout: post
keywords: blog
description: blog
title: java经典排序算法总结
categories: work
tags: 冒泡排序、选择排序、插入排序、希尔排序、归并排序、快速排序、堆排序。
---

### 背景

经典排序算法在面试笔试中占有很大一部分，作为要出去找工作的毕业生来说，很多都已经忘记了。。其实这也是基础，所以加上自己的理解再巩固一下吧！

---

### 冒泡排序

1.自我理解

* 1．比较相邻的前后二个数据，如果前面数据大于后面的数据，就将二个数据交换。

* 2．这样对数组的第0个数据到N-1个数据进行一次遍历后，最大的一个数据就“沉”到数组第N-1个位置。

* 3．N=N-1，如果N不为0就重复前面二步，否则排序完成。

2.代码

{% highlight java %}
	public static void bubbleSort(int[] source) {
		int length = source.length;
		for (int i = 0; i < length - 1; i++) {
			for (int j = 0; j < length - 1 - i; j++) {
				if (source[j] > source[j + 1]) {
					swap(source, j, j + 1);
				}
			}
		}
		printArray(source);
	}

	public static void swap(int[] source, int x, int y) {
		int temp = source[x];
		source[x] = source[y];
		source[y] = temp;
	}

	public static void printArray(int[] source) {
		for (int i = 0; i < source.length; i++) {
			System.out.print("\t" + source[i]);
		}
	}
{% endhighlight %}

### 选择排序

1.自我理解

* 1.在未排序序列中找到最小（大）元素，存放到排序序列的起始位置。

* 2.再从剩余未排序元素中继续寻找最小（大）元素，然后放到已排序序列的末尾。

* 3.以此类推，直到所有元素均排序完毕。

2.代码

{% highlight java %}
	public static void selectSort(int[] source) {
		int length = source.length;
		int minIndex = 0;
		for (int i = 0; i < length - 1; i++) {
			minIndex = i;
			for (int j = i + 1; j < length; j++) {
				if (source[j] < source[minIndex]) {
					minIndex = j;
				}
			}
			if (minIndex != i) {
				swap(source, minIndex, i);
			}
		}
		printArray(source);
	}
{% endhighlight %}

### 快速排序

1.自我理解

**挖坑填数+分治法**

2.代码

{% highlight java %}
	public static int[] quickSort(int[] source, int l, int r) {
		if (l < r) {
			int i = l, j = r, x = source[l];
			while (i < j) {
				while (i < j && source[j] >= x)
					j--;
				if (i < j) {
					source[i++] = source[j];
				}
				while (i < j && source[i] < x)
					i++;
				if (i < j) {
					source[j--] = source[i];
				}
			}
			source[i] = x;
			quickSort(source, l, i - 1);
			quickSort(source, i + 1, r);
		}
		return source;
	}
{% endhighlight %}

### 总结

<img src="/image/sort.png"/>
