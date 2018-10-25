---
layout: post
title: Java将List按照指定大小分成多个List
subtitle: 
date: 2018-03-13
categories: java
tags: [java]
description: Java将List按照指定大小分成多个List。
---

#### Java将List按照指定大小分成多个List
> 需求：有一个list集合，将该list集合分成每几个一个List。

- 方法一

```Java

package com.cnsyear;

import java.util.ArrayList;
import java.util.List;

/**
 * list分割工具类
 * 
 * @author jiebaobao
 *
 */
public class ListUtils {

	/**
	 * 分割list
	 * 
	 * @param list
	 * @param pageSize
	 * @return
	 */
	public static <T> List<List<T>> splitList(List<T> list, int pageSize) {
		List<List<T>> listArray = new ArrayList<>();

		// 实现思路：类似分页
		int count = list.size();// 总数
		int pageCount = (count + (pageSize - 1)) / pageSize;// 总页数

		for (int i = 0; i < pageCount; i++) {// 按照页数来遍历
			List<T> subList = new ArrayList<>();
			for (int j = 0; j < count; j++) {
				int pageIndex = ((j + 1) + (pageSize - 1)) / pageSize; // 当前记录的页码(第几页)
				if (pageIndex == (i + 1)) { // 当前记录的页码等于要放入的页码时
					subList.add(list.get(j)); // 放入list中的元素到分割后的list(subList)
				}
				if ((j + 1) == ((i + 1) * pageSize)) { // 当放满一页时退出当前循环
					break;
				}

			}
			listArray.add(subList); // 将分割后的list放入对应的数组的位中
		}

		return listArray;
	}

	/**
	 * 测试
	 * 
	 * @param args
	 */
	public static void main(String[] args) {
		//
		List<String> list = new ArrayList<>();
		for (int i = 1; i < 22; i++) {
			list.add("[" + i + "]");
		}

		List<List<String>> list2 = ListUtils.splitList(list, 10);

		int index = 1;
		for (List<String> strlist2 : list2) {
			System.out.println(index++);
			System.out.println("----------------------------------");
			for (String str : strlist2) {
				System.out.print(str + "\t");
			}
			System.out.println("END");
			System.out.println();
		}
	}

}


输出：

1
----------------------------------
[1]	[2]	[3]	[4]	[5]	[6]	[7]	[8]	[9]	[10]	END

2
----------------------------------
[11]	[12]	[13]	[14]	[15]	[16]	[17]	[18]	[19]	[20]	END

3
----------------------------------
[21]	END



```

- 方法二 效率有很大提升

```Java

package com.cnsyear;

import java.util.ArrayList;
import java.util.List;

/**
 * list分割工具类
 * 
 * @author jiebaobao
 *
 */
public class ListUtils2 {

	/**
	 * 分割list
	 * 
	 * @param list
	 * @param pageSize
	 * @return
	 */
	public static <T> List<List<T>> splitList(List<T> list, int pageSize) {
		List<List<T>> listArray = new ArrayList<List<T>>();
		List<T> subList = null;
		for (int i = 0; i < list.size(); i++) {
			if (i % pageSize == 0) {// 每次到达页大小的边界就重新申请一个subList
				subList = new ArrayList<T>();
				listArray.add(subList);
			}
			subList.add(list.get(i));
		}
		return listArray;
	}
	

	/**
	 * 测试
	 * 
	 * @param args
	 */
	public static void main(String[] args) {
		//
		List<String> list = new ArrayList<>();
		for (int i = 1; i < 22; i++) {
			list.add("[" + i + "]");
		}

		List<List<String>> list2 = ListUtils2.splitList(list, 10);

		int index = 1;
		for (List<String> strlist2 : list2) {
			System.out.println(index++);
			System.out.println("----------------------------------");
			for (String str : strlist2) {
				System.out.print(str + "\t");
			}
			System.out.println("END");
			System.out.println();
		}
	}

}


输出：

1
----------------------------------
[1]	[2]	[3]	[4]	[5]	[6]	[7]	[8]	[9]	[10]	END

2
----------------------------------
[11]	[12]	[13]	[14]	[15]	[16]	[17]	[18]	[19]	[20]	END

3
----------------------------------
[21]	END




```


 
[原文链接](http://bianrongxin.iteye.com/blog/1354350)

*标记：我们真正需要恐惧的是恐惧本身
——罗斯福*