# jest

- [参考链接1](https://zhuanlan.zhihu.com/p/150236310)
- [参考链接2](https://www.cnblogs.com/SamWeb/p/11454923.html)

## jest识别的测试文件是什么样子？

| 格式                          | 例子        |
| ----------------------------- | ----------- |
| 以 `.test.js` 结尾            | xxx.test.js |
| 以 `.spec.js` 结尾            | xxx.spec.js |
| 放到 `__test__`文件夹中的文件 | xxx.js      |



## 基本语法

### describe函数：表示一组用例

```js
describe('测试组名称',()=>{
    it('测试名称',()=>{
        // 测试用例执行代码
    })
	
    test('测试名称2',()=>{
        // 测试用例执行代码
    }
})
```

### test函数 或 it 函数：用来描述一个测试用例。

```js
test('测试用例名称',()=>{
    // 测试用例执行代码
})

it('测试用例名称2',()=>{
	// 测试用例执行代码
})
```

### expect函数：返回用例的执行结果

```js
test('test expect',()=>{
	expect('val').toBe('val')
})
```

### toBe函数：断言(jest管他叫做matcher)

- toBe用的是JavaScript中的Object.is()，为绝对相等，属于ES6中的特性，所以不能检测对象

```js
test('test01',()=>{
    expect('haha').toBe('haha') // 测试成功
    
    expect('haha').toBe('haha!') // 测试失败
})
```

### toEqual函数：同toBe函数

- 要检测对象的值的话，需要用到toEqual。toEqual递归检查对象或者数组中的每个字段

```js
test('test02',()=>{
	const data = {one:1}
    data['two'] = 2
    expect(data).toEqual({one:1,two:2})
})
```

### 特殊情况


| 函数          | 含义                |
| :------------ | :------------------ |
| toBeNull      | 只匹配null          |
| toBeUndefined | 只匹配undefined     |
| toBeDefine    | 与toBeUndefined相反 |
| toBeTruthy    | 匹配任何if语句为真  |
| toBeFalsy     | 匹配任何if语句为假  |

### 数字匹配

| 函数                   | 含义                   |
| ---------------------- | ---------------------- |
| toBeGreaterThan        | 大于                   |
| toBeGreaterThanOrEqual | 大于或等于             |
| toBeLessThan           | 小于                   |
| toBeLessThanOrEqual    | 小于或等于             |
| toBeCloseTo            | 对比两个浮点数是否相等 |

```js
test('two plus two',()=>{
    const value=2+2
    expect(value).toBeGreaterThan(3)
    expect(value).toBeGreaterThanOrEqual(3.5)
    expect(value).toBeLessThan(5)
    expect(value).toBeLessThanOrEqual(4.5)
    
    // toBe and toEqual are equivalent for numbers
    expect(value).toBe(4)
    expect(value).toEqual(4)
})

test('两个浮点数字相加',()=>{
    const value = 0.1 +0.2
    expect(value).toBeCloseTo(0.3)
})
```

### toMatch函数：字符串——正则表达式

```js
test('there is no I in team',()=>{
    expect('team').not.toMatch(/I/)
})

test('but there is a "stop" in Christoph',()=>{
    expect('Christoph').toMatch(/stop/)
})
```

### toContain函数：检测数组中是否包含特定某一项

```js
const shoppingList = [
    'diapers',
    'kleenex',
    'trash bags',
    'paper towels',
    'beer'
]

test('购物清单里有啤酒',()=>{
    expect(shoppingList).toContain('beer')
})
```

### toThrow函数：测试特定函数的时候抛出一个错误

```js
function compileAndroidCode(){
    throw new ConfigError('you are using the wrong JDK')
}

test('compiling android goes as expected',()=>{
    expect(compileAndroidCode).toThrow()
    expect(compileAndroidCode).toThrow(ConfigError)
    
    // You can also use the exact error message or a regexp
    expect(compile)
})
```

