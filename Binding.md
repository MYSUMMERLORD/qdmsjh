## 事件绑定与取消（前端面试江湖） ##

（一）、写一个通用的事件侦听器。

	<p id='f_p' name='drunk'>come<span>xixixi</span>on</p>
	<button id = "bind" onclick="alert('summer 点击了绑定事件捕获');bind(document.getElementsByTagName('p')[0],'click',myClick,true)">p标签绑定事件捕获</button>
	<button id = "bind" onclick="alert('summer 点击了绑定事件冒泡');bind(document.getElementsByTagName('p')[0],'click',myClick,false)">p标签绑定事件冒泡</button>
	<!--<button id = "unbind" onclick="unbind(document.getElementsByTagName('p')[0],'click')">p标签解绑事件</button>-->
	<button id = "unbind" onclick="document.getElementsByTagName('p')[0].removeEventListener('click',myClick,true)">p标签解绑事件</button>


	<script type="text/javascript">
		//绑定事件与取消绑定
		var handleHash = {}; //记录各个type对应的handle
		var captureHash = {};  //记录各个type对应的handle的事件类型
		var bind = (function(){
			if(window.addEventListener){
				return function(el,type,fn,capture){
					el.addEventListener(type,fn,capture);
					handleHash[type] = handleHash[type] || [];
					handleHash[type].push(fn);
					capture = capture || false;
					captureHash[type] = captureHash[type] || [];
					captureHash[type].push(capture);
				};
			}else if(window.attachEvent){
				return function(el,type,fn,capture){
					el.attachEvent("on"+type,fn);
					handleHash[type] = handleHash[type] || [];
					handleHash[type].push(fn);
					capture = capture || false;
					captureHash[type] = captureHash[type] || [];
					captureHash[type].push(capture);
				};
			}
		})();
		//根据type取消相关的handle
		var unbind = (function(){
			if(window.addEventListener){
				return function(el,type,fn,capture){
					if(handleHash[type]){
						for(var i = 0 ;i < handleHash[type].length ;i ++){
							el.removeEventListener(type,handleHash[type][i],captureHash[type][i]);
						}
					}
				};
			}else if(window.attachEvent){
				return function(el,type){
					if(handleHash[type]){
						for(var i = 0 ;i < handleHash[type].length ;i ++){
							el.detachEvent(type,handleHash[type][i]);
						}
					}
				};
			}
		})();
		var i = 0;
		function myClick(){
			alert(++i);
		}
	</script>
	</body>
	</html>

`注意`：

1. 书中的代码不太对，因为如果要移除事件句柄，`addEventListener（）`的执行函数必须使用外部函数，如上面的myClick，匿名函数，类似`"document.removeEventListener('event',function(){});"`该事件是无法移除的。
2. 除此之外，如果在`addEventListener`的时候，设置事件类型为true，则在解绑的时候，也必须设置第三个参数为true。如果add的时候没有指定，也就是默认的，则解绑的时候，也可以不指定事件类型。