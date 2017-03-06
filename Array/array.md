## 数组相关的题目 ##
1. 编写函数，用于过滤一个数组内重复的元素，并用这些元素重构一个新数组，新数组内也不能有重复元素。
		function Unique(arr){
			var newArr = [];
			for(var i = 0;i < arr.length; i++){
				if(newArr.join(",").indexOf(arr[i]) == -1){
		  			newArr.push(arr[i]);
				}else{
		  			arr.splice(i,1);
		  			i--;
				}
				}
				console.log(arr); //[ 1, 2, 3, 4, 5 ]
				console.log(newArr); //[ 1, 2, 3, 4, 5 ]
		}
		Unique([1,2,3,4,5,2,1]);
2. 