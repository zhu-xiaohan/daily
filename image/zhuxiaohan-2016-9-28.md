#集合的使用
===============================

* 集合类的结构图和主要用法

* 掌握方法
	
	  * 如何创建
	  
	  * 如何添加元素
	  
	  * 如何修改元素
	  
	  * 如何删除元素
	  
	  * 如何遍历 
	
* 泛型：规范类型
  	
  
*  list

	* ArrayList  可变数组
	
		import java.util.ArrayList;
		import java.util.Iterator;
		import java.util.List;
    	* LinkedList 链表
	
		* 在集合任何位置（头部、中间、尾部）添加、获取
		
		* 插入、删除操作频繁时，可使用LinkedList来提高效率
		
		* LinkedList还额外提供对头部和尾部元素进行添加和删除操作的方法 
    * set
	
	* Set接口也是Collection接口的子接口，但是与Collection或List接口不同的是，Set接口中不能加入重复的元素。
	
	* Set接口的定义： public interface Set<E> extends Collection<E>
	
	* Set接口的主要方法与Collection是一致的 
	
	* Set接口的实例无法像List接口那样进行双向输出
	
	* Set接口的常用子类 
	
		* HashSet (散列的存放) :
		  
		  HashSet是Set接口的一个实现类，
		  主要的特点是：
			里面不能存放重复元素，
			采用散列的存储方式，所以是没有顺序(插入顺序)的。
      * map 

	* HashMap
	
	package com.feicuiedu.demo3;

	import java.util.HashMap;
	import java.util.Iterator;
	import java.util.Map;
	import java.util.Set;

	
			
