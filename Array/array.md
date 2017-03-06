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
