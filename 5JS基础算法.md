# JS基础算法

#### 1.翻转字符串

```JS
function reverseString(str) {
  let strArr = str.split('');//字符串->数组元素
  strArr = strArr.reverse().join('');//反转元素并转换为字符串
  return strArr;
}

reverseString("hello");
console.log(reverseString("hello"))
```

#### 2.整数阶乘

```JS
function factorialize(num) {
  return num > 0 ? num * factorialize(num - 1) : 1;
}
//递归
factorialize(5);
```

#### 3.找出多个数组中的最大数字

```js
function largestOfFour(arr) {
  let narr = [];
  for (let i = 0; i < arr.length; i++) {
    let max = arr[i][0];
    for (let j = 1; j < arr[i].length; j++) {
      if (arr[i][j] > max)
        max = arr[i][j];
    }
    narr.push(max);
  }
  arr=narr;
  return arr;
}

console.log(largestOfFour([[17, 23, 25, 12], [25, 7, 34, 48], [4, -10, 18, 21], [-72, -3, -17, -10]]));

```

#### 4.确认结尾

```JS
//法一
function confirmEnding(str, target) {
  if (str.slice(str.length - target.length) === target) {
	//if (str.slice(- target.length) === target)
    return true
  } 
    return false;
}
confirmEnding("Bastian", "n");
console.log(confirmEnding("Bastian", "n"))
```

[法二](./3正则表达式(使用JS).md#min-content)

```JS
//法三
function confirmEnding(str, target) {
  if(str.endsWith(target)) {
    return true;
  }else{
    return false;
  }
}
```

#### 5.重复输出

```JS
function repeatStringNumTimes(str, num) {
  let nstr="";
  for(let i=0;i<num;i++){
    nstr+=str;
  }
  return nstr
  //递归
  //return num>0?str+repeatStringNumTimes(str,num-1):""; 
  //repeat方法
  /*
  function repeatStringNumTimes(str, num) {
  if(num <=0) {
    str = "";
  }else{
    str = str.repeat(num);
  }
  return str;
  
}
  */  
  
}

repeatStringNumTimes("abc", 3);
```

#### 6.截断字符串

```JS
//法一
function truncateString(str, num) {
  if(num<str.length){
    let nstr = ""
  for (let i = 0; i < num; i++) {
    nstr += str[i];
  }
  str = nstr+"...";
  }
  return str;
}

//法二
function truncateString(str, num) {
  if(num<str.length){
    return str.slice(0,num)+"...";
  }
  return str;
  //return str.length>num?str,slice(0,8)+"...":str;
}

truncateString("A-tisket a-tasket A green and yellow basket", 8);



```

#### 7.基本类型布尔值检查

```JS
function booWho(bool) {
  // return bool === true || bool === false ? true : false;
  return typeof (bool) == "boolean"
}

booWho(null);
console.log(booWho(null))

```

#### 8.句中首字母大写

```JS
function titleCase(str) {
  let nstr = str.split(" ");//字符串转单词数组
  for (let i = 0; i < nstr.length; i++) {
    nstr[i]=nstr[i].toLowerCase().split('');//单词全换为小写，转字母数组
    nstr[i][0] = nstr[i][0].toUpperCase();//首字母大写
    nstr[i]=nstr[i].join('');//字母数组转单词字符串
  }

  return nstr.join(' ');
}

titleCase("I'm a little tea pot");
```

