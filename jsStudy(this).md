# hahaha ZT
JavaScript拥有一个名为this 的关键字，在JavaScript程序中的不同位置，this所引用的值会有所不同。

1、在全局上下文中

当你在全局上下文中(也就是说不在任何函数中)引用this 会发生什么？

console.log(this === window); // true  	
全局上下文中的this 指向了window 对象。观察下面的代码以及随后的输出：

this.message = "Check this out.";
window.message = "Check this out.";

console.log(this.message); // "Check this out."
console.log(window.message); // "Check this out."
console.log(message); // "Check this out."	
2、在函数上下文中

当你在函数或是闭包中引用了this 结果又会如何？

在这个没有任何嵌套的函数中，this值取决于你是否使用了严格模式：

function checkThisOut () {
  console.log(this === window); // true
  console.log(this); // object global
}
checkThisOut();	
你可以看到，这与在全局上下文中没有任何变化(就是说this 依然引用了window对象)

function checkThisOut () {
  "use strict"; //严格模式，为了防止意外的声明全局变量
  console.log(this === window); // false
  console.log(this); // undefined
}

checkThisOut();	
 
3、在模块模式中
让我们来看看在一个这种模式的上下文中 this 值引用了什么。

var s,
  PrimaryNameSpace = {

    settings : {
      first: true,
      second: false,
      foo: 'bar'
    },

    init: function () {
      console.log(this); // references PrimaryNameSpace
    },

    nextMethod: function () {
    },

    anotherMethod: function () {
    }

  };

PrimaryNameSpace.init();	
在模块模式上下文中，每一个单独方法(即函数)中，this 将引用整个模块。
因此，在 init() 方法中，你能够以下列方式使用 this 来引用模块及配置：

/* ... other code here ...*/

  init: function () {
    s = this.settings;
    this.nextMethod();
    this.anotherMethod();
    console.log(s);            
  },

/* ... other code here ...*/

PrimaryNameSpace.init();	
如果你在众多方法之一里包含了一个匿名函数，那么 this就会发生变化，你将无法通过 this来访问模块对象。此时就需要书写长形式的语法，如下所示：

/* ... other code here ...*/


对于一个嵌套函数呢？
如果你在众多方法之一里包含了一个匿名函数，那么 this就会发生变化，你将无法通过 this来访问模块对象。此时就需要书写长形式的语法，如下所示：

/* ... other code here ...*/

  init: function () {
    s = this.settings;
    (function () {
      this.nextMethod();
      // [object Window] has no method 'nextMethod'
    })();
  },

/* ... other code here ...*/	

