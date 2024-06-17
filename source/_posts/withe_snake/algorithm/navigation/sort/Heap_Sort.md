---
title: 堆排序
date: 2022-06-26 09:19:17
tags:
- 排序算法
- 基础
categories:
- 算法
- 排序算法
---
# 堆排序
堆分为最小堆和最大堆两种，我们这里只记录下最小堆：

![最小堆排序，插入元素](http://pic.xishng.top/img/202201171553440.jpg)

最小堆排序，插入元素

![堆排序示意图](http://pic.xishng.top/img/202201171553439.gif)

代码实现：

```golang
package main

import "fmt"

func heapsort(nums []int) []int {
	lenght := len(nums)
	if lenght == 0 {
		return nil
	}
	for i := 0; i < lenght; i++ {
		// 第一下 使得第一个元素最小，接下来就从第二个来构造，使得下一个最小，
		miniHeap(nums[i:])
	}
	return nums
}

// 使得每次操作完毕 堆顶的元素就是最小的，由于堆的特性，我们只需要从倒数第二层开始就可以了
func miniHeap(nums []int) {
	length := len(nums)
	floor := length/2 - 1
	for i := floor; i >= 0; i-- {
		// 然后比较的每一个节点与其两个孩子节点的大小，使得爸爸永远是最小的
		// 有一种特殊情况，就是最后一个节点的孩子节点可能不存在，和可能只有一个，所以需要加上一个判断
		baba := i
		left := 2*i + 1
		right := 2*i + 2

		if right < length && nums[baba] > nums[right] {
			nums[baba], nums[right] = nums[right], nums[baba]
		}

		if left < length && nums[baba] > nums[left] {
			nums[baba], nums[left] = nums[left], nums[baba]
		}

		//if left < length && right < length && nums[left] > nums[right]{
		//	nums[left], nums[right] = nums[right], nums[left]
		//}
	}
}

func top10() {
	// 30 * 10 = 300
	bigData := []int{
		3, 231, 321, 1, 7, 3, 45, 6, 2, 23,
		1, 31, 23, 1, 312, 67, 45, 3, 43, 435,
		32, 13, 56, 78, 500, 467, 321, 543, 23, 10,
		12, 12, 32, 321, 321, 43, 54, 65, 76, 45,
		67, 8, 45, 87, 32, 78, 4, 90, 45, 34,
		32, 13, 56, 78, 510, 467, 321, 543, 23, 11,
		12, 12, 32, 321, 301, 43, 55, 65, 76, 45,
		12, 12, 32, 321, 31, 43, 54, 65, 76, 45,
		12, 12, 32, 321, 321, 4, 54, 65, 76, 45,
		12, 12, 32, 321, 321, 43, 54, 65, 76, 45,
		12, 12, 32, 321, 321, 43, 4, 65, 76, 45,
		2, 12, 32, 321, 321, 43, 54, 65, 76, 45,
		12, 12, 32, 321, 321, 43, 54, 65, 76, 45,
		12, 12, 32, 321, 321, 43, 4, 65, 7, 45,
		12, 12, 32, 321, 321, 43, 5, 65, 6, 45,
		12, 12, 32, 321, 321, 43, 54, 65, 76, 45,
		12, 12, 32, 301, 321, 43, 4, 65, 76, 45,
		712, 32, 32, 321, 321, 43, 54, 65, 7, 45,
		612, 12, 32, 321, 321, 43, 54, 65, 76, 45,
		512, 12, 32, 401, 321, 43, 54, 65, 76, 45,
		212, 12, 32, 1, 321, 43, 54, 65, 76, 45,
		12, 12, 32, 321, 321, 43, 54, 65, 76, 45,
		12, 12, 32, 371, 321, 43, 54, 65, 76, 45,
		12, 12, 32, 321, 321, 453, 54, 65, 76, 45,
		12, 12, 32, 321, 321, 43, 554, 65, 76, 45,
		12, 172, 32, 301, 321, 43, 54, 65, 76, 45,
		12, 192, 32, 321, 321, 43, 564, 65, 76, 45,
		12, 142, 32, 321, 321, 43, 54, 65, 76, 45,
		12, 12, 32, 21, 321, 43, 54, 605, 76, 45,
		12, 122, 632, 321, 301, 43, 54, 65, 76, 495,
	}
	fmt.Println("the big data is ", bigData)
	startNums := bigData[:10]
	miniHeap(startNums)
	for _, data := range bigData[10:] {
		if data <= startNums[0] {
			continue
		} else {
			startNums[0] = data
			miniHeap(startNums)
		}
	}
	fmt.Println("top10 is ", heapsort(startNums))
}

```

from: [golang:排序-堆排序-解决百万数据top100问题](https://zhuanlan.zhihu.com/p/366379441)