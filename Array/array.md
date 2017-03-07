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
2. 编写一个javascript函数fn，该函数有一个参数n（数字类型），其返回值是一个数组，该数组内是n个随机且不重复的整数，且整数取值范围是[2,32].

	** 写代码的原则：可用、健壮、可靠（例如出现异常，该怎么做，可以输入[]等）、宽容、精益求精 **

		function getRand(min,max){
			var range = max - min;
			var random = Math.random();
			return min + Math.round(range * random);
		}
		
		function checkInArr(arr,val){
			if(arr.indexOf(val) !== -1){
				return true;
			}else{
				return false;
			}
		}
		function isThere(n){
			if(n == null || n == undefined){
				return false;
			}else{
				return true;
			}
		}
		function typeOk(n){
			if(isNaN(Number(n)) || typeof(n) == 'string' && n.trim().length == 0){
				return false;
			}else{
				return true;
			}
		}
		function initialN(n){
			return Math.round(Number(n));
		}
		function rangeOk(n,min,max){
			if(n< min || n > max){
				return false;
			}else{
				return true;
			}
		}
		function getRandomN(n){
			//健壮性校验
			if(!isThere(n)) return [];
			if(!typeOk(n)) return [];
				//对数字进行归一化
			n = initialN(n);
			if(!rangeOk(n,2,32)) return [];
			//准备一个容器保存结果
			var arr = [];
			//循环
			for(var i = 0; i < n ; i++){
				//创建一个随机数
				var rnd = getRand(2,32);
				//检查是否重复
				if(checkInArr(arr,rnd)){
					i--;
				}else{
					arr.push(rnd);
				}
			}
			return arr;
		}
		console.log(getRandomN(4.653232323));
3. 先有一个数组（元素为数字，并且有可能重复），请给Array.prototype增加一个方法（方法名自取），该方法能去掉数组中全部最小和最大的数字。

		Array.prototype.removeOutlier = function(){
		    var max = Math.max.apply(null,this);
		    var min = Math.min.apply(null,this);
		    for(var i = 0 ; i< this.length; i++){
		        if(this[i] == min || this[i] == max){
		        	this.splice(i,1);
		        	i--;
		    	}
		    }
		  	return this;
		}
		var arr = [1,2,3,4,5];
		console.log(arr.removeOutlier());
4. 给定一个数组实现字符串反转，要求原地实现。
		
		//Array本来就有reverse方法，所以这里是让自己实现内置的reverse方法
		function reverse(arr){
		    var temp;
		    for(var i = 0; i < arr.length / 2; i ++){
		    	console.log(i);
		    	temp = arr[i];
		    	arr[i] = arr[arr.length - i - 1];
		    	arr[arr.length - i - 1] = temp;
		    }
		    return arr;
		}
		console.log(5/2); // 2.5
		console.log(reverse([1,2,3,4,5])); // [ 5, 4, 3, 2, 1 ]
5. 如何判断一个JavaScript对象是数组

		var arr = [1,2,3,4,5];
		//1#
		if(Object.prototype.toString.call(arr) == '[object Array]'){
		    console.log("a 是数组");
		}else{
		    console.log("a 不是数组");
		}
		//2#
		if(arr.constructor == Array){
		    console.log("a 是数组");
		}else{
		    console.log("a 不是数组");
		}
		//3#
		if(arr instanceof Array){
		    console.log("a 是数组");
		}else{
		    console.log("a 不是数组");
		}
		console.log(arr.constructor); // function Array()
6. 请写一个函数，功能是删除数组的指定下标元素。（输入可以是多个下表构成的字符串（删除单个元素相对简单））

		Array.prototype.Unique = function(){
		    var arr = this;
		    var newArr = [];
		    for(var i = 0;i < arr.length; i++){
		        if(newArr.join(",").indexOf(arr[i]) == -1){
		          newArr.push(+arr[i]); //+：把后面的字符串转化为数字
		        }
		    }
		    return newArr;
		}
		Array.prototype.Delete = function(index){
		  	//假设传过来的是一个字符串，该字符串中包含若干个数组下标，用逗号分隔
		  	//判断是否为空
		  	if(index == null || index == undefined) return []; //isNaN([1,2,3]) 竟然输出true
		  	var arr = index.split(",");
		  	arr = arr.Unique();
		  	//对下标集合按递增排序，方便后面按顺序删除指定元素
		  	arr.sort(function(a,b){return a-b;});
		  	//判断所指定的下标集合里面是否有不在length范围内的，如果超出范围内，则直接返回空，或给出提示
		  	if(Math.min.apply(null,arr) < 1 || Math.max.apply(null,arr) > this.length) return [];
		  	for(var i = j = arr[0]-1,n=0;i<this.length-arr.length;i++){ //i和j是原数组的下标索引（i：被替换的位置，j：要替换的位置），n是指下标集合数组的索引
    			while(j == arr[n] - 1){    ////上面这句话好绕口
		        	n++;
		        	j++;
		    	}
		    	this[i] = this[j];
		    	j++;
		  	}
		  	this.length -= arr.length;
		  	return this;
		}
		var arr = [1,2,3,4,5,6,7];
		var input = "6,1,2,3,4,11";
		console.log(arr.Delete(input));
7. 请写一个函数removeVoid(arr)，删除该数组中值为"null, undefined"的项，返回原数组。

		function removeVoid(arr){
		  for(var i = 0;i < arr.length;i++){
		    if(arr[i] == null || arr[i] == undefined){
		      arr.splice(i,1);
		      i--;
		    }
		  }
		  return arr;
		}
		var arr = [1,2,,3,4,null,4,3,undefined,,]; //javascript识别中间的空,,数组末尾的空自动舍去
		
		console.log(arr.length);  // 10
		console.log(arr[2] == true);  // false
		console.log(typeof arr[2]);  //undefined
		console.log(arr[3]);  //3
		console.log(removeVoid(arr)); //[ 1, 2, 3, 4, 4, 3 ]