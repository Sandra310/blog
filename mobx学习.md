### 用法
### 源码 mobx

```
f (typeof Proxy === "undefined" || typeof Symbol === "undefined") {
    throw new Error("xxx")
}
```
mobx依赖ES6的Proxy与Symbol

#### Symbol
Symbol的出现是为了解决属性名字的独一无二，是第7种数据类型，类似于字符串
```
let s = Symbol()  
typeof s //symbol

let s1 = Symbol('foo') //用于控制台显示或转为字符串做区分
s1 //symbol(foo)
```
Symbol不能运算，能转为string或bool，不能转number

```
String(s1) // symbol(foo)
s1.toString() // symbol(foo)
Boolean(s1) // true
!s1 // false
```

主要用法：
```
let mySymbol = Symbol();

// 第一种写法
let a = {};
a[mySymbol] = 'Hello!';

// 第二种写法
let a = {
  [mySymbol]: 'Hello!'
};

// 第三种写法
let a = {};
Object.defineProperty(a, mySymbol, { value: 'Hello!' });

// 以上写法都得到同样结果
a[mySymbol] // "Hello!"
```

### 源码 mobx-react
