---
title: Android代码中动态设置LayoutParam
date: 2017-10-24 09:36:17
tags: android
categories: anodroid
---

## Android 代码中动态设置LayoutParam

android中每个控件自身的位置由其自身的LayoutParam控制自身的属性，通过LayoutParam可以设置布局的宽，高，相对位置，grivty属性等等。如何设置和改变LayoutParam

#### 1. 新建一个LayoutParam
	第一个参数为宽的设置，第二个参数为高的设置。    
	LinearLayout.LayoutParams p = new LinearLayout.LayoutParams(    
		LinearLayout.LayoutParams.FILL_PARENT,    
		LinearLayout.LayoutParams.WRAP_CONTENT);    
	//调用addView()方法增加一个TextView到线性布局中    
	mLayout.addView(textView, p);
	
	
#### 2. 获取View的LayoutParam
	ViewGroup.MarginLayoutParams layoutParams = (ViewGroup.MarginLayoutParams) viewHolder.mRelateLayout.getLayoutParams(); 
	layoutParams.setMargins(ScreenUtils.dip2px(15), ScreenUtils.dip2px(10), ScreenUtils.dip2px(15), ScreenUtils.dip2px(20));
	
	
##注意点：
setLayoutParam是子对父的，也就说父布局下要设置子布局的LayoutParam时候要强转成父布局Param.若父控件是RelativeLayout则需要强制转换RelativeLayout.LayoutParams，其它类型依次类推。
