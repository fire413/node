# ES5与ES6的继承

## ES5的继承

```js
   function Phone(brand,price){
      this.brand=brand;
      this.price=price;
    }
    Phone.prototype.calling=function(){
      console.log("拨打电话")
    }
    function SmartPhone(brand,price,color,size){
      // 函数的方法call()
      Phone.call(this,brand,price)           //-----------相当于写了this.brand=brand;this.price=price;
      this.color=color;
      this.size=size;
    }
    console.log(Phone.prototype);
    SmartPhone.prototype=new Phone();  // 给SmartPhone赋原型，SmartPhone也有了brand，price属性，以及call方法
    SmartPhone.prototype.photo=function(){
      console.log("正在拍照");
    }
    var iPhone=new SmartPhone("苹果",9999,"黑色","13英寸");
    console.log(iPhone);
    iPhone.calling();
```

## ES6的继承

```js
    class Phone{
      constructor(brand,price){
        this.brand=brand;
        this.price=price;
      }
      call(){
        console.log("拨打电话");
      }

      // get与set
      get config(){
        console.log("get");
         return '64';
      }
      set config(val){
        console.log("set");
      }
    }
    var phone=new Phone();
    phone.config="4+64";  //set
    console.log(phone.config);   // get 64

    class SmartPhone extends Phone{
      constructor(brand,price,color,size){
        // Uncaught ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor
        super(brand,price);
        this.color=color;
        this.size=size;
      }
      photo(){
        console.log("正在拍照");
      }

      // 子类重写父类的方法
      call(){
        console.log("视频通话");
      }
    }

    var smartphone=new SmartPhone("苹果",9999,"黑色","13英寸");
    smartphone.call();
```

ES5与ES6除写法外的区别：

1. `class` 声明会提升，但不会初始化赋值。`Foo` 进入暂时性死区，类似于 `let`、`const` 声明变量。
2. `class` 声明内部会启用严格模式。
3. `class` 的所有方法（包括静态方法和实例方法）都是不可枚举的。
4. `class` 的所有方法（包括静态方法和实例方法）都没有原型对象 prototype，所以也没有`[[construct]]`，不能使用 `new` 来调用。
5. `class` 内部无法重写类名。













