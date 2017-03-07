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
2. 已知对象var obj = {......}，但对象的属性未知，如何对该对象的属性进行遍历。

		var Summer = {
		  name: 'juan',
		  age: 25,
		  skill: 'IT',
		  write: function () {
		    console.log('Hello');
		  }
		};
		function scanObj(obj) {
		  //存放属性信息
		  var propertyArr = [
		  ];
		  //开始遍历
		  for (var property in obj) {
			//注意啊，这里后面的function要加双引号，不加双引号，js引擎就会认为这是function关键字，后面肯定要跟（）{}，所以就提示错误
		    if (typeof obj[property] == "function" ) {
		      obj[property];
		    } else {
		      propertyArr.push(property + '=' + obj[property]);
		    } 
		  }
		  console.log(propertyArr);
		}
		scanObj(Summer);
3. 创建对象的方法 （ **来自前端面试江湖** ）

	（1）原始方法
	
		var obj = new Object();
		obj.name = "summer";//为对象添加属性
		obj.age = 25;
		obj.showName = function(){ //为对象添加方法
			console.log(this.name);
		}
		obj.showName(); //summer
		
	以上方法通过new关键字生成了一个对象，然后根据JavaScript是动态语言的特性来添加属性和方法，构造一个对象。其中的this表示调用该方法的对象。
	
	`缺点：如果需要多次创建对象，那么需要重复代码多次，不利于代码的复用`

	(2) 工厂方法

		function createObj(){
			var obj = new Object(); //创建对象
			obj.name = "summer";//为对象添加属性
			obj.age = 25;
			obj.showName = function(){ //为对象添加方法
				console.log(this.name);
			}
			return obj;//返回对象
		}
		var obj = createObj();
		obj.showName();//summer
		
	`缺点：参数不能变,代码复用率低`

	(3) 工厂方法的一点改进

		function createObj(name, age){
			var obj = new Object(); //创建对象
			obj.name = name;//为对象添加属性
			obj.age = age;
			obj.showName = function(){ //为对象添加方法
				console.log(this.name);
			}
			return obj;//返回对象
		}
		var obj = createObj("summer",25);
		obj.showName();//summer

	`缺点：虽提高了代码复用率，但和面向对象中类的概念相比，有一个很大的缺陷。面向对象强调对象的属性私有，但对象的方法是共享的。而上面的工厂方法在创建对象时，要为每个对象创建各自私有的方法。同时，由于为每个对象都创建逻辑相同的方法，所以很浪费内存。`
	针对以上方法，再作适当的改进。
		
		function createObj(name, age){
			var obj = new Object(); //创建对象
			obj.name = name;//为对象添加属性
			obj.age = age;
			obj.showName = showName;
			return obj;//返回对象
		}
		function showName(){ //为对象添加方法
				console.log(this.name);
			}
		var obj = createObj("summer",25);
		obj.showName();//summer

	`上述方法通过定义几个函数对象，解决了不同对象持有函数对象的私有问题，现在所有对象的方法都持有上面两个函数的引用。但这么一来，对象的函数又和对象相互独立了，这和面向对象中特定方法属于特定类的思想不符合。`

	(4) 构造函数方法

		function Person(name, age){
			this.name = name;//为对象添加属性
			this.age = age;
			this.showName = function showName(){ //为对象添加方法
				console.log(this.name);
			}
		}
		
		var obj = new Person("summer",25);
		obj.showName();//summer

	`构造函数的方法和工厂方式一样，会为每个对象创建独享的函数对象。当然也可以将这些函数对象定义在函数外面，这样又有了对象和方法相互独立的问题。`
	
	(5) 原型方法
	`该方法把所有属性和方法都通过原型来构造，也就是说属性和方法都是共享的。所以，首先，该方法的问题是构造函数不能传递参数，每个新生成的对象都有默认值。其次，方法共享没问题，但是，当属性是可变状态的对象时，属性共享就有问题了。`
	(6) 混合方法（构造函数+原型方法）
	`该方法是将私有属性通过构造函数构造，共享方法通过原型方式构造。例子有很多，这里就不列举了。`
