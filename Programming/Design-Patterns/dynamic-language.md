
# 第一部分：面向对象的JavaScript

- 动态语言的特点        

动态类型语言区别于静态类型语言的特点是，编译的时候无需类型检查，变量    
是没有类型的，类型在对象身上，而对象只有在执行时才会知道类型，所谓类型，是一种存储结构   
比如 栈是连续的内存地址的一段空间，可以存储不可变的类型数据，如数字。堆是散列的内存地址集合   
用与存储可变类型数据，如对象，数组，函数。    

（1） 鸭子类型    

由于动态语言天生就忽略了类型检查，对象的类型就不必关注（比如静态语言编写函数时，函数的参数都要事先定义好类型，    
动态语言则不必），只关注对象的方法，有一种很抽象的说法---鸭子类型。    
（不必关注对象的类型是什么，只关注对象的特征（方法），只要叫声像鸭子，就可以当作是鸭子。）

（2） 面向接口编程    

那么由于忽略类型检查带来的鸭子类型这个特性，有什么好处或者应用场景呢？答案是：“面向接口”的编程方式---面向接口编程。
（使用鸭子类型的思想，能不必借助超类型的帮助，实现面向接口编程，但接口检查依旧要写逻辑判断，或者使用Typescript）  
面向接口编程： 同一个执行者，可以调用很多命令，对不同的命令会产生不同的结果。这种代码组织方式，背后的思想是多态。

- 多态

这里说的多态，是说对象的多态性。不同类型的对象可以拥有相同名字的方法，就是对象的多态性（前提是绕开了类型检查），
所以鸭子类型是多态的一种，另一种实现多态的方式是继承。     
多态的本质是：不变和变化的部分抽离开（解耦），然后封装变化的部分，使得程序有了可扩展性，符合开放-封闭原则。        


-  封装数据

JavaScript没有提供private、public等关键字的语法解析来封装数据，只能依赖变量作用域来实现封装特性.
```js
var myObject = (function(){ 
    var __name = 'sven'; // 私有（private）变量
    return { 
        getName: function(){ // 公开（public）方法
            return __name; 
        } 
    } 
})(); 
console.log( myObject.getName() ); // 输出：sven 
console.log( myObject.__name ) // 输出：undefined
```
（1） 封装实现

封装使得对象之间的耦合变松散，对象之间只通过暴露的 API 接口来通信。当我们修改一个对象时，可以随意地修改它的
内部实现，只要对外的接口没有变化，就不会影响到程序的其他功能。拿迭代器来说明，迭代器的作用是在不暴露一个聚合对象的
内部表示的前提下，提供一种方式来顺序访问这个聚合对象

（2） 封装类型

封装类型是静态类型语言中一种重要的封装方式。一般而言，封装类型是通过抽象类和接口
来进行的，当然在 JavaScript 中，并没有对抽象类和接口的支持，对于 JavaScript 的设计模式实
现来说，不区分类型是一种失色，也可以说是一种解脱。

（3） 封装变化

从意图上区分，设计模式分别被划分为: 创建型模式、结构型模式和行为型模式。    

创建型模式（比如原型模式）:要创建一个对象，是一种抽象行为，而具体创建什么对象则是可以变化
的，创建型模式的目的就是封装创建对象的变化。

而结构型模式封装的是对象之间的组合关系。

行为型模式封装的是对象的行为变化。

通过封装变化的方式，把系统中稳定不变的部分和容易变化的部分隔离开来，在系统的演变
过程中，我们只需要替换那些容易变化的部分，如果这些部分是已经封装好的，替换起来也相对容易。
这可以最大程度地保证程序的稳定性和可扩展性

- 原型模式和基于原型继承的JavaScript对象系统

原型模式不仅仅是一种设计模式，也是一种编程范型。JavaScript 就是使用原型
模式来搭建整个面向对象系统的。在 JavaScript 语言中不存在类的概念，对象也并非从类中创建出来的，
所有的 JavaScript 对象都是从某个对象上克隆而来的。


