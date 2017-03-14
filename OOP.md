## JavaScript中的面向对象 ##
1. JavaScript中new的作用？
2. JavaScript中的对象类比java面向对象中的类
		
		function f2(){
		  //类的私有成员
		  var a1 = "I am a parentClass field!";
		  //类的公有成员
		  this.a2 = 3;
		  this.b2 = 4;
		}
		function f1(){
		  this.al = 1;
		  this.b1 = 2;
		}
		//类的prototype属性也是一个对象，下面定义的是其所包含的方法
		f2.prototype.method = function(){
		  console.log("我是f2原型的method方法");
		}
		f1.prototype = new f2();
		//上面这条语句的意思是：1.执行函数f2创建了一个对象，
		//然后把这个对象赋值给f1的原型
		//2.把右边类的原型prototype赋值给左边的__proto__属性
		objF1 = new f1();

---
		//为了验证上面说的第一条，给f1的prototype属性加一个方法
		f1.prototype.methodf1 = function(){
		  console.log("我是f1原型的method方法");
		}	

输出f1.prototype ：Object { a2: 3, b2: 4 }，也就是说把f1原来prototype属性里的methodf1给覆盖掉了