layout: post
title: Javascript 内置函数
date: 2014-10-21
category: 技术
tags: 
keywords: 
description: 项目中用到的，正好看书的时候碰到了，记录一下。
---

### javascript数字验证方法

#### Number()

将括号内的变量的值转换为数字。

<!-- more -->

#### isNaN(n)

检验*n*是否为数字（浮点或整型），如果不是则返回true。

#### parseFloat(n)

将*n*转换为浮点数。它从左向右依次解析字符串中的每个字符，直至在数字中无法使用的字母，然后停止，将字符串转换为数字。如果第一个字符在数字中就无法使用，结果就是NaN，表示非数字（Not A Number）。

#### parseInt(n)
		
通过直接把小数部分移除而不考虑四舍五入，将*n*转化为整数。任何传到这个函数当中的非数字字符都会被丢弃掉。如果第一个字符不是+，-或数字，结果就是NaN。

### code sample

		function isNubmer(){
			var total = document.getElementById('total');
			if(!total){	return false;	}
			total = total.value;
			if(total.length === 0){
				alert('Field is empty!');
				return false;
			}
			if(isNaN(total)){
				alert('Please input a number!');
				return false;
			}
			return true;
		}
