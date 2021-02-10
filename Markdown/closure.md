# Closure - 闭包的作用

## 1.返回值

- 以闭包的形式将name返回。

```js
function fn(){
    var name = "hello";
    return function(){
        return name;
    }
}

var fnc = fn();
console.log(fnc());
```

## 2.函数赋值

- 在闭包里面给fn2函数设置值，闭包的形式吧name属性记忆下来，执行会输出hello。

```js
var fn2;
function fn(){
    var name="hello";
    // 将函数赋值给fn2
    fn2 = function(){
        return name;
    }
}
fn(); // 要先执行进行赋值
console.log(fn2()) // 执行输出fn2
```

## 3.函数参数

- 用闭包返回一个函数，把此函数作为另一个函数的参数，在另一个函数里面执行这个函数，最终输出 hello

```js
function fn(){
    var name="hello";
    return function callback(){
        return name;
    }
}
var fn1 = fn() // 执行函数将返回值(callback函数)赋值给fn1

function fn2(f){
    // 将函数作为参数传入
    console.log(f()) // 执行函数，并输出
}
fn2(fn1) // 执行输出fn2
```

## 4.IIFE(自执行函数)

```js

```