![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501112015579.png)

## mockjs介绍

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501112016231.png)

## 基本使用

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501112017043.png)
![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501112020053.png)

## 核心用法

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501112021057.png)

## 数据生成规则

### 数据生成模板 DTD

mock 语法规范中的每个属性由 3 部分构成：属性名 name、生成规则 rule、属性值 value

```json
'name|rule': value
```

属性名和生成规则之间用 竖线 `|` 分隔，生成规则是可选的
生成规则有 7 种格式：

```json
'name|min-max': value
'name|count': value
'name|min-max.dmin-dmax': value
'name|min-max.dcount': value
'name|count.dmin-dmax': value
'name|count.dcount': value
'name|+step': value
```

- 生成规则的含义需要依赖属性值的类型才能确定
- 属性值中可以含有 @占位符
- 属性值还指定了最终类的初始值和类型

### 生成规则和示例

1. 属性值是字符串 string
```json
// 通过重复 string 生成一个字符串，重复次数大于等于 min，小于 max，
'name|min-max': string

// 通过重复 string 生成一个字符串，重复次数等于count
'name|count': string
```

```js
var data = Mock.mock({
	'name|1-3': 'a', // 重复生成 1到3个 a (随机)
	'name2|2' : 'b' // 生成 bb
})
```

2. 属性是数字 number
```json
// 属性值自动加 1，初值为 number
'number|+1': number

// 生成一个大于等于 min、小于 max 的整数，属性值 number 只是用来确定类型
'number|min-max': number

// 生成一个浮点数，整数部分大于等于 min，小于 max，小数部分保留到 dmin 到 dmax 位，
'name|min-max.dmin-dmax': number
```

```js
Mock.mock({
	'number1|1-100.1-10': 1,
	'number2|1223.1-10': 1,
	'number3|123.3': 1,
	'number4|123.10': 1.123
})


// 结果
{
	"number1": 12.92,
	"number2": 123.51,
	"number3": 123.777,
	"number4": 123.1231091814
}
```

```js
var data = Mock.mock({
	'name1|+1': 4,      // 生成4，如果循环每次加1
	'name2|1-7': 2,     // 生成一个数字，1到7之间
	'name3|1-4.5-8': 1  // 生成一个小数，参数部分1到4，小数部分5到8位，数字1只是为了确定类型
})
```

3. 属性值是对象 Object

```json
// 随机生成一个布尔值，值为 true 的概率是 1/2，值为 false 的概率同样是 1/2
'name|count': object

// 随机生成一个布尔值，值为 value 的概率是 min/(min + max)，值为 !value 的概率是 max/(min + max)
'name|min-max': value
```

4. 属性值是对象 Object

```json
// 从属性值 object 中随机选取 count 个属性
'name|count': object

// 从属性值 object 中随机选取 min 到 max 个属性
'name|min-max': object
```

```js
var obj = {
	a: 1,
	b: 2,
	c: 3,
	d: 4
}
var data = Mock.mock({
	'name|1-3': obj,  // 随机从 obj 中寻找 1到3 个属性，新对象
	'name|2': obj     // 随机从 obj 中寻找两个属性，新对象
})
```

5. 属性值是数组 Array

```json
// 从属性值 array 中的随机选取 1 个元素，作为最终值，
'name|1': array

// 从属性值 array 中的顺序选取 1 个元素，作为最终值，
'name|+1': array

// 通过重复属性值 array 生成一个新数组，重复次数大于等于 min，小于等于 max.
'name|min-max': array

// 通过重复属性值 array 生成一个性数组，重复次数为 count
'name|count': array
```

```js
Mock.mock({
	// 通过重复属性值 array 生成一个新数组，重复次数为 1-3 次
	"favorite_game|1-3": [3, 5, 4, 6, 23, 28, 42, 45],
});
```

```js
var arr = [1, 2, 3];
var data = Mock.mock({
	'name|1': arr,  // 从数组里随机取出1个值
	'name|2': arr,  // 数组重复 count 次，这里 count 为2
	'name|1-3': arr, // 数组重复 1到3 次
})
```

6. 属性值是函数 Function

```json
// 执行函数 function，取其返回值作为最终的属性值，函数的上下文属性 'name' 所在的对象
'name': function
```

7. 属性值是正则表达式 RegExp

```json
// 根据正则表达式 regexp 反向生成可以匹配他的字符串，用于生成自定义格式的字符串
'name': regexp
```

```js
Mock.mock({
	'regexp1': /[a-z][A-Z][0-9]/,
	'regexp2': /\w\W\s\S\d\D/,
	'regexp3': /\d{5,10}/
})
// =>
{
	"regexp1": "p37",
	"regexp2": "F)\fp1G",
	"regexp3": "561659409"
}
```

### 占位符 DPD

占位符只是在属性值字段中战歌位置，并不出现先在最终的属性值中，

占位符的格式为：

```js
@占位符
@占位符(参数 [, 参数])
```

 关于占位符需要知道以下几点
- 用 `@` 标识符后面的字符串是占位符
- 占位符引用的是 `Mock.Random` 中的方法
- 可以通过 `Mock.Random.extend()` 来拓展自定义占位符。
- 占位符 也可以引用 数据模板 中的属性
- 占位符 支持 相对路径 和 绝对路径

```js
// 引入 mockjs
import Mock from 'mockjs'
// 使用 mockjs 模拟数据
Mock.mock('/api/...', {
	"ret": 0,
	"data": 
	{
		"mtime": "@datetime", // 随机生成日期时间
		"score": "@natural(1, 800)", // 随机生成1-800的数字
		"rank": "@natufal(1, 100)", // 随机生成1-100的数据
		"rank": "@natural(1, 5)", // 随机生成1-5的数字
		"nickname": "@cname", // 随机生成中文名字
	}
});
```

![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501120851724.png)
![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501120852974.png)
![image.png](https://cdn.jsdelivr.net/gh/03xiaoyuhe/PicStore/img/202501120853961.png)


