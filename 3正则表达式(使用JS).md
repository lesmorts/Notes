# JS正则:ghost:

### 1.测试匹配项

.test()方法：成功匹配字符返回TRUE 反之返回FALSE；

```js
let myString = "Hello, World!";
let myRegex = /Hello/;//正则表达式
let result = myRegex.test(myString);//测试

```

### 2.提取匹配项

.match()方法是  .test()方法的反向

```js
"Hello, World!".match(/Hello/);
let ourStr = "Regular expressions";
let ourRegex = /expressions/;
ourStr.match(ourRegex);
```



### 3.操作符

- ##### 或：|

/dog|cat/

- ##### 通配符：.

/.un./

- ##### 字符集：[]

/h[uo]g/

/[a-z0-9]/  匹配a到z和0到9范围内的字符

- ##### 否定字符集：

/^[a-z0-9]/   匹配非字母和非数字字符

- ##### 匹配一个或多个字符：+

/a+/  匹配 abc 返回 ["a"]  匹配aabc 返回["aa"] 匹配abac 返回["a","a"] 

- ##### 匹配零个或多个字符: *

/Go*/

- ##### 字符串开头

/^a/

- ##### 字符串末尾

/$/

- ##### 短语元字符：匹配所有字母和数字和 '_'字符

/\w/

匹配所有除字母和数字以外的字符

/\W/

- ##### 匹配所有数字

/\d/

匹配所有非数字

/\D/

- ##### 匹配空格、回车符、制表符、换页符和换行符

\s == [ \r\t\f\n\v]

匹配非空格、回车符、制表符、换页符和换行符

\S== [ ^\r\t\f\n\v]

- ##### 数量说明符

匹配出现 `3` 到 `6` 次字母 `h` 的字符串 `Ohhhhh no`

/Oh{3,6} no/

匹配包含四个或更多字母 `z` 的单词 `Hazzzzzzah`

/Haz{4,}ah/

匹配仅有四个字母 `m` 的单词 `Timmmmber`

/Tim{4}ber/

- ##### 检查前面的零个或一个元素

匹配美式英语（`favorite`）和英式英语（`favourite`）的单词版本

/favou?rite/

- ### 删去字符串开头和结尾的空白

/^\s+|\s+$/

- ## 先行断言

##### 正向

匹配大于5个字符且有两个连续数字

/(?=\w{6,})(?=.*\d{2})/

### 4.标志

- ##### 忽略大小写：i

/dog/i

- ##### 全局匹配:g

/Repeat/g

### 5.贪婪(greedy)匹配和懒惰(lazy)匹配

```js
let text = "<h1>Winter is coming</h1>";
let myRegex = /<.*>/;//greedy 结果为"<h1>Winter is coming</h1>"
let myRegex = /<.*?>/;//lazy 结果为"<h1>"
```



## 6.捕获组

- #### 分组匹配的子字符串被保存到一个临时的“变量”， 可以使用同一正则表达式和反斜线及捕获组的编号来访问它（例如：`\1`）。 捕获组按其开头括号的位置自动编号（从左到右），从 1 开始。

- #### 在字符串上调用 `.match()` 方法将返回一个数组，其中包含它最终匹配到的子字符串及其捕获组。

```js
//通过把要捕获的正则表达式放在括号中来构建
let repeatNum = "42 42 42";

let reRegex = /^(\d+) \1 \1$/; // 使用捕获组来匹配一个只由相同的数字重复三次组成的由空格分隔字符串。
let result = reRegex.test(repeatNum);//Returns true
repeatNum.match(reRegex); // Returns ["42 42 42", "42"]
```



###  7.例题

- 需要检索数据库中的所有用户名。 以下是用户在创建用户名时必须遵守的一些简单规则。


1. 用户名只能是数字字母字符。
2. 用户名中的数字必须在最后。 数字可以有零个或多个。 用户名不能以数字开头。
3. 用户名字母可以是小写字母和大写字母。
4. 用户名长度必须至少为两个字符。 两位用户名只能使用字母。

```js
let username = "JackOfAllTrades";
let userCheck = /^[a-z][a-z]+\d*$|^[a-z]\d+\d+$/i; // 或 /^[a-z]([a-z]+\d*$|\d+\d+)$/i

let result = userCheck.test(username);
```



- <span id="min-content">确认结尾</span>

  ```JS
  function confirmEnding(str, target) {
      //使用RegExp函数课传入动态参数
      //其中正则表达式符号需要转义
    var reg=new RegExp('\.'+target+"\$");
    return reg.test(str);
  }
  
  console.log(confirmEnding("Bastian", "n"));
  ```

  

