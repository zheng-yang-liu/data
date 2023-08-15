# 第九章 js面向对象

## 一、对象

### 一）对象的概念

类是一种引用类型的数据结构，它将将数据和功能组织在一起。

对象是某个特定引用类型的实例。

### 二）对象的创建

#### 1、基于Object的方式创建对象

```
var 对象名称=new Object( );
```

```
var user = new Object();
    user.name = "张三";
    user.pwd = "123456";
    user.show=function(){document.write(this.name+"-"+this.pwd);}
user.show();

```

#### 2、使用对象字面量创建对象

对象字面量是创建对象的一种简写形式，简化创建包含大量属性的对象的过程，为函数传递大量可选参数时，可考虑使用对象字面量。

```
var user = {
        name:"张三",
        pwd:"123456",
        show:function(){
            document.write(this.name+"-"+this.pwd+"<br/>");
        }
    }
    user.show();

```

### 三）工厂模式创建对象

#### 1、工厂模式创建对象

软件工程领域的一种设计模式，抽象了创建对象的过程，通过函数封装创建对象的细节。

```
function createUser(name,pwd){
        var user = new Object();
        user.name = name;
        user.pwd = pwd;
        user.show=function(){
            document.write(this.name+"-"+this.pwd+"<br/>");
        }
        return user;
    }
    var user1 = createUser("张三","123456");
    var user2 = createUser("李四","654321");
    user1.show();
    user2.show();
```

#### 2、工厂模式创建对象存在的问题

- 看不出类型--解决：构造函数
- 函数重复、浪费资源--解决：原型

## 二、构造函数

### 一）构造函数特征

- 构造函数一般以大写字母开头
- 构造函数也是函数，只不过可以用来创建对象
- 与工厂模式对比
- 没有显式创建对象
- 直接将属性和方法赋给了this对象
- 没有return

### 二）使用构造函数创建对象示例

```
function User(name,pwd){
	this.name = name;
        this.pwd = pwd;
        this.show=function(){
            document.write(this.name+"-"+this.pwd+"<br/>");
        }
    }
    var user1 = new User("张三","123456");
    var user2 = new User("李四","654321");
    user1.show();
    user2.show();
```

## 三、原型

### 一）原型概念

每个函数都有一个prototype（原型）属性，函数原型是一个指针，指向一个对象，这个对象（函数的原型对象）的用途是包含可以由特定类型的所有实例共享的属性和方法。

在默认情况下，所有原型对象都会自动获得一个constructor(构造函数)属性，这个属性是一个指向prototype属性所在函数的指针。

```
<script>
	function Person(name,age){
		this.name=name;
		this.age=age;
	}
	alert(Person.prototype) //验证结果，弹出[object object],函数的原型是一对象
	Person.prototype.sayHi=function(){alert("Hi!")}
	alert(Person.prototype.constructor);//弹出的结果是Person函数
</script>
```



### 二）原型应用

```
function User(name,pwd){
        this.name = name;
        this.pwd = pwd;
    }
User.prototype.show=function(){
        document.write(this.name+"-"+this.pwd+"<br/>");
};
var user1 = new User("张三","123456");
var user2 = new User("李四","654321");
user1.show();
user2.show();
```

## 四、继承

### 一）原型链继承-prototype

#### 1、原型、原型对象，对型对象的构造函数

![](prototype-constructor.png)

#### 2、子对象.prototype=new 父对象构造函数()

```
function Person(){
	this.foot=2;
	this.head=1;
}
function Studuent(name,no){
	this.name=name;
	this.no=no;
}
Student.prototype=new Person();
Student.prototype.constructor=Student;
var stu1=Student("张三","s001")
console.log(stu1.name);
console.log(stu1.no);
console.log(stu1.foot);
console.log(stu1.head);
```

#### 3、原型链继承-prototype

由于Person对象中，**不变的属性都可以直接写入Person.prototype。**所以，可以让Student()跳过 Person()，直接继承Person.prototype

优点：效率比较高,不用执行和建立Person的实例
缺点：Student.prototype和Person.prototype现在指向了同一个对象，任何对Student.prototype的修改，都会反映到Person.prototype

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>继承-直接继承prototype属性</title>
</head>
<body>
<script>
    function Person(){
    }
    Person.prototype.foot = 2;
    Person.prototype.head = 1;
    function Student(name,no){
        this.name=name;
        this.no=no;
    }
    //通过直接继承prototype属性,相较第一种，不用执行和建立Person实例，节省内存
    Student.prototype = Person.prototype;
    //手工理顺一下继承链
    Student.prototype.constructor = Student;
    //每个实例的prototype对象都有一个constructor属性
    //alert(Student.prototype.constructor);
    //继承链紊乱
    var stu1 = new Student("张三","s001");
    alert(stu1.constructor);
    alert(stu1.name);
    alert(stu1.no);
    
    alert(stu1.foot);
    alert(stu1.head);

    //缺点：把父类Person的constructor也同步改掉了
    alert(Person.prototype.constructor);
</script>
</body>
</html>
```

#### 4、利用空对象作为中介

空对象几乎不占用内容，修改Student的原型对象不会影响不会影响到Person的原型对象。

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>继承-直接继承prototype属性</title>
</head>
<body>
<script>
    function Person(){
    }
    Person.prototype.foot = 2;
    Person.prototype.head = 1;
    function Student(name,no){
        this.name=name;
        this.no=no;
    }
    var F=function(){};
    F.prototype=Person.prototype;
    Student.prototype=new F();
    var stu1=new Student("张三","s001");
    Student.prototype.constructor=Student;
    console.log(stu1.name);
    console.log(stu1.no);
    console.log(stu1.foot);
    console.log(stu1.head);
    //空对象解决了前面的问题:把父类Person的constructor 也同步改掉的问题。
    console.log(Person.prototype.constructor);   
</script>
</body>
</html>
```

#### 5、利用空对象作为中介—封装为函数

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title>继承-直接继承prototype属性</title>
</head>
<body>
<script>
   function Person(){
}
Person.prototype.foot = 2;
Person.prototype.head = 1;
function Student(name,no){
    this.name=name;
    this.no=no;
}
function extended(Child,Parent){
    var F=function(){};
    F.prototype=Person.prototype;
    Child.prototype=new F();
    Child.prototype.constructor=Child;

}
extended(Student,Person);
var stu1=new Student("张三","s001");
alert(stu1.constructor);
alert(stu1.name);
alert(stu1.no);

alert(stu1.foot);
alert(stu1.head);
</script>
</body>
</html>
```

### 二）构造函数绑定

通过call()或apply()方法在子类型构造函数的内部调用父类型构造函数。通过call()方法把父类的this指向子类的this，这样就可以实现子类继承父类属性。

```
<Script>
  function Person(str){
      this.school=str;
      this.hi=function(){
          console.log("Hello "+str);
      }
}
function Student(name,no,add){
    //Person.call(this,add);
    //Person.call(this,"新龙科技集团")
    Person.apply(this,add);
    this.name=name;
    this.no=no;
}

var n=new Student("刘能","s001",["保定电力职业技术学院"]);
console.log(n.school);
console.log(n.name);
console.log(n.no);
n.hi();
</Script>
</Script>
```

```
function.call(thisObj[, arg1[, arg2[, [,...argN]]]])调用一个对象的一个方法，以另一个对象替换当前对象。例如：B.call(A, args1,args2);即A对象调用B对象的方法
function.apply(thisObj[, argArray])应用某一对象的一个方法，用另一个对象替换当前对象。例如：B.apply(A, arguments);即A对象应用B对象的方法
两方法产生的作用相同，传参不同,apply的参数是一个数字
```

#### 三)组合继承和拷贝继承

#### 1、组合继承

也叫伪经典继承，它将原型链继承和构造函数继承组合在一起。原型链继承实现对原型属性和方法的继承；借用构造函数实现对实例属性的继承。

```
<Script>
  function Person(){
    this.foot = 2;
    this.head=1;
     this.favorColor=["red","yellow"];
}
 Person.prototype.sayColor=function(){
     alert("Hello,我最爱的颜色是："+this.favorColor);
 }
function Student(name,no){
    //使用构造函数绑定实现了对父类属性的继承
    Person.call(this);
    this.name=name;
    this.no=no;
}
 //原型链继承-继承property对象的属性和方法
Student.prototype = new Person();
Student.prototype.constructor = Student;
 var stu1 = new Student("张三","s001");
 alert(stu1.foot);
 alert(stu1.head);
 alert(stu1.favorColor);

 var stu2 = new Student("李四","s002");
 alert(stu2.foot);
 alert(stu2.head);
 alert(stu2.favorColor);
</Script>
```

#### 2、拷贝继承

把父对像的所有属性和方法，拷贝进子对象，将父对象的原型对象（prototyper指向的对象）的属性，一一拷贝给子对象的原型对象（即子对象的prototype指向的对象）。

```
<Script>
   function Person(){}
   Person.prototype.foot = 2;
   Person.prototype.head = 1;
   Person.prototype.saySelf=function(){
       alert("Hello,我有："+this.foot+"只脚和"+this.head+"个头");
   }
   function Student(name,no){
       this.name = name;
       this.no = no;
   }
   //拷贝继承
   function extend2(Child,Parent){
       var p = Parent.prototype;
       var c = Child.prototype;
       for(var i in p){
           c[i] =p[i];
       }
   }
   extend2(Student,Person);
   var stu1 = new Student("张三","s001");
   alert(stu1.foot);
   alert(stu1.head);
   alert(stu1.name);
   alert(stu1.no);
   stu1.saySelf();
</Script>
```

