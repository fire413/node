*new*运算符都做了哪些操作呢？ 1、创建了一个**新对象**（是Object类型的数据） 2、将this指向新对象 3、将创建的对象的原型指向构造函数的原型 4、返回一个对象（如果构造函数本身有返回值且是对象类型，就返回本身的返回值，如果没有才返回新对象）

```js
/**
 \* 模拟实现 new 操作符
 \* @param {Function} ctor [构造函数]
 \* @return {Object|Function|Regex|Date|Error}   [返回结果]
 */
function newOperator(ctor){
  // 判断参数
  if(typeof ctor !== 'function'){
   throw 'newOperator function the first param must be a function';
  }
  // ES6 new.target 是指向构造函数
  newOperator.target = ctor;

  // 创建一个新对象，并链接到该函数的prototype上
  let newObj = Object.create(ctor.prototype);
  // 除去ctor构造函数的其余参数
  var argsArr = [].slice.call(arguments, 1);
  // 生成的新对象绑定到函数调用的this
  var ctorReturnResult = ctor.apply(newObj, argsArr);
  // 如果有返回则返回，无返回则直接返回该新对象
  var isObject = typeof ctorReturnResult === 'object' && ctorReturnResult !== null;
  var isFunction = typeof ctorReturnResult === 'function';
  if(isObject || isFunction){
​    return ctorReturnResult;
  }
  // 5.如果函数没有返回对象类型`Object`(包含`Functoin`, `Array`, `Date`, `RegExg`, `Error`)，那么`new`表达式中的函数调用会自动返回这个新的对象。
  return newObj;
}
function Student(name, age){
  this.name = name;
  this.age = age;
  // this.doSth();
  // return Error();
}
Student.prototype.doSth = function() {
  console.log(this.name);
};
var student1 = newOperator(Student, '张', 18);
var student2 = newOperator(Student, '三', 18);
// var student1 = new Student('张');
// var student2 = new Student('三');
console.log(student1, student1.doSth()); // {name: '张'} '张'
console.log(student2, student2.doSth()); // {name: '三'} '三'
student1.__proto__ === Student.prototype; // true
student2.__proto__ === Student.prototype; // true
// __proto__ 是浏览器实现的查看原型方案。
// 用ES5 则是：
Object.getPrototypeOf(student1) === Student.prototype; // true
Object.getPrototypeOf(student2) === Student.prototype; // true
```

