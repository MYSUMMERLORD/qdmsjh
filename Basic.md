## 基础题 ##

1. 注意下面的**"list" + arr** = list数组元素

		var name = "zhangsan";
		function GetName(){
		    var arr = [1,2,3];
		    var name = "list" + arr;
		    console.log(name);
		    console.log(arr);
		}
		GetName();  // print list1,2,3
		document.write(name); //Arrary [1,2,3]
		console.log(name); //zhangsan