## 代码有问题，不知道出在哪里 ##

	<!DOCTYPE html>
	<html>
	<head>
		<title>hello,summer</title>
		<meta charset="utf-8" />
	</head>
	<body>
	
	<div>
		<p id='f_p' name='drunk'>come<span>xixixi</span>on</p>
		<a href="http://www.baidu.com">百度</a>
		<button id = "bind" onclick="alert('summer 点击了绑定事件捕获');alert(bind);bind(document.getElementsByTagName('p')[0],'click',myClick,true)">p标签绑定事件捕获</button>
		<button id = "bind" onclick="alert('summer 点击了绑定事件冒泡');alert(bind);bind(document.getElementsByTagName('p')[0],'click',myClick,false)">p标签绑定事件冒泡</button>
		<!--<button id = "unbind" onclick="unbind(document.getElementsByTagName('p')[0],'click')">p标签解绑事件</button>-->
		<button id = "unbind" onclick="document.getElementsByTagName('p')[0].removeEventListener('click',myClick,true)">p标签解绑事件</button>
	</div>
	<script type="text/javascript">
		/*alert(window.event);
		document.getElementsByTagName('p')[0].onclick = function(e){
			alert("我是第一个handle");
	
		}
		document.getElementsByTagName('p')[0].onclick = function(e){
			alert("我是第二个handle");
	
		}
		*/
		/*	
		document.getElementsByTagName('div')[0].addEventListener('click',function(e){alert(" i am div");},true);
		document.getElementsByTagName('div')[0].addEventListener('click',function(e){alert(" 我是div的第二个handle");},true);
		document.getElementsByTagName('div')[0].addEventListener('click',function(e){alert(" i am div");},false);
		document.getElementsByTagName('span')[0].addEventListener('click',function(e){alert('i am span');},true);
		document.getElementsByTagName('span')[0].addEventListener('click',function(e){alert('i am span');},false);
		*/
		/*var atts = document.getElementsByTagName('p')[0].attributes;
		console.log(atts);
		//console.log('the length of atts is '+atts.length);
		for (var i = 0;i<atts.length;i++) {
			console.log(atts[i].nodeName+'='+atts[i].nodeType+'\n');
		}
		console.log(document.getElementsByTagName('p')[0].children);*/
		/*var obj = document.getElementsByTagName('span')[0];
		obj.onclick = function(){
			alert("this is a click")
		}
		obj.onmouseover = function(){
			alert("this is mouse over");
		}
		*/
		//document.getElementsByTagName('a')[0].attachEvent('onclick',function(e){alert("this is a");alert(this);e.preventDefault();});
	
	
		//绑定事件与取消绑定
		var handleHash = {};
		var bind = (function(){
			if(window.addEventListener){
				return function(el,type,fn,capture){
					el.addEventListener(type,function(){
						alert("执行事件绑定中。。。")
						fn();
						handleHash[type] = handleHash[type] || [];
						handleHash[type].push(fn);
					},capture);
				};
			}else if(window.attachEvent){
				return function(el,type,fn,capture){
					el.attachEvent("on"+type,function(){
						fn();
						handleHash[type] = handleHash[type] || [];
						handleHash[type].push(fn);
					});
				};
			}
		})();
		//根据type取消相关的handle
		var unbind = (function(){
			if(window.addEventListener){
				return function(el,type){
					alert("正在解绑");
					alert(el+"-"+type);
					if(handleHash[type]){
						for(var i = 0 ;i < handleHash[type].length ;i ++){
							el.removeEventListener(type,handleHash[type][i]);
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