说一下  Object.defineProperty 

```
es5.js 中定义如下

/**
@param {Object} obj
@param {PropertyKey} prop
@param {Object} desc
@param {boolean} [desc.configurable = false]
@param {boolean} [desc.enumerable = false]
@param [desc.value]
@param {boolean} [desc.writable = false]
@param {Function} [desc.get]
@param {Function} [desc.set]
@static
@return {Object}
*/
Object.defineProperty = function(obj,prop,desc) {};
```
这个是给Object这个对象(函数)添加一个属性(函数类型的)有三个参数分别是 obj对象 string的key 以及对象类型descpritor


#3作用:给一个对象添加可配置的属性
默认情况下我们给对象通过以下类似的方法添加属性

```
var p = {
	name:'xxx',
	age: 20
}
p.height = 170
```
但是从面向对象的思想来看添加的属性不具备可读可写等配置例如java等其他语言可以设置属性是readonly 可以设置在调用属性的时候其实是在调用对象的set,get方法 由此es5新增的```Object.defineProperty```可以用来进行配置属性的读写setget in 等操作


第一个参数： obj : 要添加属性的对象


第二个参数： key: 属性的名字

第三个参数： obj： 属性相关的配置信息包括两种情况

1.当属性是一个数据属性的时候

```
// 可以在 typescript中的 lib.es6.d.ts中查看到

interface PropertyDescriptor {
    configurable?: boolean; // 是否可以delete删除 修改以及改变类型 数据属性还是访问器属性
    enumerable?: boolean; // fo(var i in obj)的是否是否可以遍历出来
    value?: any; // 默认的值 
    writable?: boolean; // 可读写配置
```

2.当属性是一个访问器属性的时候

```
   configurable?: boolean; // 同上
    enumerable?: boolean; // 同上
    get? (): any; // 当调用属性值的时候调用的get函数
    set? (v: any): void; //当设置属性的时候调用的set函数
    
    // tip: 基本上和java 以及swift等语言一样了
```

例子：

```
//  'use strict';

  var obj = {
      name : ''
  };
  Object.defineProperty(obj,'name',{
      'configurable': false,
      'enumerable': false,
      set: function (newValue) {
        console.log(newValue+'haha');
      },
      get: function () {

      }
  });
  obj.name = 20;
  for(var i in obj){
    console.log(i);
  }
  console.log(obj.name);

```

需要注意的时候如果一个属性你设置成只读的但是你还要进行赋值操作 非严格模式下不会赋值成功也不报错 严格模式下会抛出异常

当然也可以进行多个属性的赋值:```Object.defineProperties()```

