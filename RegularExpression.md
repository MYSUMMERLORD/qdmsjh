## 正则表达式相关的题目 ##

`学习视频`:[http://www.imooc.com/video/12538](http://www.imooc.com/video/12538 "imooc")
	
`test RegExper的网址`：[https://regexper.com/](https://regexper.com/ "regexper")

1. 请编写一个JavaScript函数parseQueryString，它的用途是把url参数解析为一个对象，如：

		function parseQueryString(url){
		  //step 1：获取参数相关的字符串
		  var para = url.split("?")[1];
		  //step 2：用相应的正则表达式分组来识别出key和value
		  var reg1 = /(\w+)\s?=\s?(\w+)/g;
		  var result = {};
		  while(item = reg1.exec(para)){
		    result[item[1]] = item[2];
		  }
		  return result;
		}
		var url = "http://www.baidu.com/index.aspx?key0=0  & key1=1&key2=2";
		var obj = parseQueryString(url);

2. 请写一个正则表达式，验证一下数列：

	1，2，3，4，5，6，7，8，9，10，11，12

		/^((1[0-2]|[0-9]),)*(1[0-2]|[0-9])/

3. 用正则表达式去掉重复的字符串，而只保留其中的一个。

	这道题不是很严谨，如果是去掉连续重复的字符串，则表达式为：

		repleace(/((.)+?)\1+/g,$1)

	如果是去掉重复的字符串（其实就是只保留出现一次的字符），则表达式为：

		replace(/((.)+)((.)*\1)+/g,$1)
		replace(/(.)((.)*\1)+/g,$1)
	
	如果是去掉重复的字符串（字符串长度至少为2），则表达式为：

		replace(/(.{2,})((.)*\1)+/g,$1)
4. 用正则表达式判断手机、邮箱、电话、中文。

 	`手机`：/^13[159]\d{8}$|^15[089]\d{8}/

	`邮箱`：/^[\w-]+@[\w-]+(\.[\w-]+)+$/

	`中文`：/^[\u4e00-\u9fa5]+$/  这里的中文包括中文、英文字符、数字、某些符号`_=?[]\^%@``

5. 使用JavaScript讲字符串中由空格隔开的每个单词首字母大写。

		str.replace(/\b\w+\b/g,function(word){
		    return word.charAt(0).toUpperCase()+word.substring(1);
		})

	`replace、slice、substr、substring`不改变原字符串



	

