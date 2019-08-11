### new 到底发生了什么

### 定义

> 在 MDN 上是这样说的：**new 运算符**创建一个用户定义的对象类型的实例或具有构造函数对象的内置对象的实例

从第一种我们可以看出，new 运算符执行了一下四步操作(MDN)
 1. 创建一个新的空的 JavaScript 对象（即{}）；
 2. 链接该对象（即设置该对象的构造函数）到另一个对象；
 3. 将步骤 1 新创建的对象作为 this 的上下文；
 4. 如果该函数没有返回对象，则返回this
 
> **注意：** 在该构造函数返回值为引用类型时，则返回该引用值，如果是基本类型时，则相当于没有返回值。

### js 模拟 new

```
  function objectFactory() {
		// 创建一个新对象
		var o = new Object();
		// 取得该函数的第一个参数（并删除第一个参数），该参数是构造函数
		var constructor = [].shift.call(arguments);
		// 将新对象的内部属性__proto__指向构造函数的原型，这样新对象就可以访问原型中的属性和方法
		obj.__proto__ = constructor.prototype;
		// 使用 apply，将构造函数中的 this 执行新对象，这样新对象就可以访问构造函数中的属性和方法
		// 并取得构造函数返回值
		var ret = constructor.apply(obj, arguments);
		// 构造函数可能存在返回 null 的情况
		return typeof ret === 'object' ? ret || obj : obj;
	}
```