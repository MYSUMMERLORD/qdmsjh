## 日期和时间（前端面试江湖） ##

1. 按照格式XXXX年XX月XX日XX时XX分XX秒动态显示时间，要求不满10的在前面补0。

		new function(){
		    with(new Date()){
		        var t = function(a){ return a< 10 ? "0"+a:a;}
		        console.log(getFullYear()+"年"+t(getMonth()+1)+"月"+t(getDate())+"日"+t(getHours())+"时"+t(getMinutes())+"分"+t(getSeconds())+"秒");
		    }
		}
	
	`注意:`上面在获取月份的语句：**getMonth() + 1**
2. 输出从当前日期起，指定天数后的日期。

		function GetDateAfter(days){
		    var dd = new Date();
		    dd.setDate(dd.getDate()+days);//获取从今天起，days后的日期
		    var y = dd.getFullYear();
		    var m = dd.getMonth() + 1;// 获取当前月份
		    var d = dd.getDate();
		    return y + "-" + m + "-" + d;
		}
		console.log(GetDateAfter(6));

	`注意：`**dd.setDate(n)**是设置当前月的某一天，如果超过本月的最大天数，则会根据日期的规则，自动更新相应的月份和年份。
	
	如果要获取星期几，通过getDay();其返回值为0~6，
		
		var day = dd.getDay();
		if(day == 0){
			return "日"；
		}else{
			return day;
		}