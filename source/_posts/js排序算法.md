---
title: js排序算法
date: 2019-03-21 13:50:24
cover: https://tva1.sinaimg.cn/large/00831rSTgy1gcewj4vv9sj30rs0ijgmf.jpg
tags:
---

```
var examplearr = [1,23,4,1,13,2,4]
//冒泡排序
function sortarr(arr) {
	for (i=0;i<arr.length-1;i++){
		for(j=0;j<arr.length-1-i;j++){
			if(arr[j] > arr[j+1]){
				var temp = arr[j]
				arr[j] = arr[j+1]
				arr[j+1] = temp
			}
		}
	}
	return arr
}

//快速排序
function quickSort(arr){
	if(arr.length<=1){
		return arr
	}
	//找基准
	var baseIndex = Math.floor(arr.length/2)
	var base = arr.splice(baseIndex,1)[0]
	var left = []
	var right = []
	//比基准小的放在left，比基准大的放在right
	for(var i = 0; i<arr.length;i++){
		if(arr[i]<= base) {
			left.push(arr[i])
		}else{
			right.push(arr[i])
		}
	}
	return quickSort(left).concat([base],quickSort(right))
}
```