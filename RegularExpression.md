## 正则表达式相关的题目 ##

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