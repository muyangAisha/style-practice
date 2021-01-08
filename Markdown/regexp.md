# 正则表达式

## js使用内置对象REGEXP支持正则表达式

1. 字面量方式:
```js
// 只替换第一个
var reg = /\bis\b/
// /g的意思：全文搜索匹配
var reg = /\bis\b/g 
```

2. 构造函数方式:
```js
// 这里\需要转义
var reg = new RegExp('\\bis\\b','g')
```

## 贪婪模式非贪婪模式

1. 贪婪模式(匹配最多情况)
```js
'12345678'.replace(/\d{3,6}/g,'X') = X78
```

2. 非贪婪模式(匹配最少情况,使用?号)
```js
'123456789'.match(/\d{3,5}?/g,'X') = ['123','456','789']
```

## 前瞻，javascript不支持后顾(后瞻、后望)
```js
// 断言部分不参与匹配，只是检查
{
  "exp(?=assert)" : "正向前瞻",
  "exp(?!assert)" : "负向前瞻",
}

// 正向前瞻例子
'a2*3'.replace(/\w(?=\d)/g,'X') = 'X2*3'
'a2*34v8'.replace(/\w(?=\d)/g,'X') = 'X2*X4X8'
// 反向前瞻例子
'a2*34vv'.replace(/\w(?!\d)/g,'X') = 'aX*3XXX'

```

## 语法
- 功能字符
```js
{
  "\\" : "转义其他字符",
  "/^" : "开头",
  "$/" : "结尾",
  "[]" : "字符类：或者的意思（对应其中的一个，就能匹配到）",
  "[^]" : "字符类：反向或者的意思(不对应其中的任何一个，才能匹配到)",
  "[a-z]" : "范围类：-在字母数字的中间表示范围，包含自身（从a到z的任意字符，都能匹配到)",
  "[a-zA-Z-]" : "例子：（a到z、A到-Z和-，都能匹配到)",
}
```

- 元字符
```js
{
  "." : "除了回车和换行的所有字符=[^\r\n]",
  "\d" : "数字=[0-9]",
  "\D" : "非数字=[^0-9]",
  "\s" : "空白符=[\t\n\x0B\f\r]",
  "\S" : "非空白符=[^\t\n\x0B\f\r]",
  "\w" : "单词字符(字母、数字、下划线)=[a-zA-Z_0-9]",
  "\W" : "非单词字符(字母、数字、下划线)=[^a-zA-Z_0-9]",
  "\b" : "匹配一个单词的边界(空格)",
  "\B" : "非单词边界",
  "\t" : "水平制表符",
  "\v" : "垂直制表符",
  "\n" : "换行符",
  "\r" : "回车符",
  "\0" : "空字符",
  "\f" : "换页符",
  "\cX" : "与X对应的控制字符(ctrl + X)",
}
```

- 数量
```js
{
  "*" : "匹配前面的子表达式0到任意数量(次)",
  "+" : "匹配前面的子表达式1到任意数量(次)",
  "?" : "匹配前面的子表达式0-1次",
  "{n}" : "匹配前面的子表达式n次",
  "{n,m}" : "匹配前面的子表达式n到m次",
  "{n,}" : "匹配前面的子表达式最少n次",
}

```

- 特殊
```js
() : 分组功能
| : 或的关系 abc|web， 和ab(c|w)eb是不一样的意思
$1-$n : 反向引用,获取分组的匹配内容
?: : 不希望捕获某些分组
```

- 修饰符
```js
{
  "g" : "global全文搜索，不添加，搜索到第一个匹配停止",
  "i" : "ignore case 忽略大小写，默认大小写敏感",
  "m" : "multiple lines 多行搜索",
}

lastIndex:从匹配成功字符的后一个位置再次开始
source:正则表达式的文本字符串
```

## REGEXP对象属性
```js
var reg=/\w/;

reg.global默认=false
reg.ignoreCase默认=false
reg.multiline默认=false
lastIndex:从匹配成功字符的后一个位置再次开始
source:正则表达式的文本字符串 ='\w'
```

## REGEXP对象方法
```js
// test 检测字符串是否匹配正则表达式
var reg2 = /\w/g;
while(reg2.test('ab')){
    console.log(reg2.lastIndex)
    //打印1和2
}

// exec 返回匹配到的数组
var reg3=/\d(\w)(\w)\d/;
var reg4=/\d(\w)(\w)\d/g;
var ts='$1az2bb3cy4dd5ee'

var ret = reg3.exec(ts)

// 0 1 1az2,a,z
console.log(reg3.lastIndex +'\t'+ret.index +'\t'+ret.toString())
// 0 1 1az2,a,z
console.log(reg3.lastIndex +'\t'+ret.index +'\t'+ret.toString())

while(ret = reg4.exec(ts)){
    // 5 1 1az2,a,z
    // 11 7 3cy4,c,y
    console.log(reg4.lastIndex +'\t'+ret.index +'\t'+ret.toString())
}
```

## String对象方法

- search()检索与正则表达式匹配的子字符串，返回第一个对应的index，这个方法不执行全局匹配，总是从字符串的开始检索
```js
// search中的1会转化为正则 /1/
'a1b2c3d1'.search（'1'）
```
- match()检索字符串，找到多个与regexp匹配的文本(**全局的g，对match影响很大**)
```js
var reg3=/\d(\w)\d/;
var reg4=/\d(\w)\d/g;
var ts='$1a2b3c4d5e'

var ret = ts.match(reg3)

// ["1a2","a"]
console.log(ret)
// 1 0
console.log(ret.index + '\t' + ret3.lastIndex)


var ret = ts.match(reg4)
// ["1a2","3c4"]，无分组的内部信息
console.log(ret)
// "undefined 0"
console.log(ret.index + '\t' + ret4.lastIndex)
}
```

- split
```js
// ["a","b","c","d"]
'a,b,c,d'.split(',')

// ["a","b","c","d","e"]
'a1b2c3d4e5'.split(/\d/)
```

- replace
```js
// a2b
'a1b'.replace('1',2)

// a2b1c1
'a1b1c1'.replace('1',2)

// a2b2c2
'a1b1c1'.replace(/1/g,2)

// a2b3c4d5e6
'a1b2c3d4e5'.replace(/\d/g,function(match,index,origin){
    // console.log(index)
    return parseInt(match)+1
})

// a2b3c4d5e6
'a1b2c3d4e5'.replace(/(\d)(\w)(\d)/g,function(match,group1,group2,group3,index,origin){
    // console.log(match)
    return group1 + group2
})
```

## 工具网站
https://regexper.com/

## 例子
```js
/^(?![a-zA-Z]+$)(?![A-Z0-9]+$)(?![A-Z\W_]+$)(?![a-z0-9]+$)(?![a-z\W_]+$)(?![0-9\W_]+$)[a-zA-Z0-9\W_]{8,30}$/
```