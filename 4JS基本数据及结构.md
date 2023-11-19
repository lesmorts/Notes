# JS基本数据及结构

1.一些函数

```js
Array.push()//加后
Array.unshift()//加前
Array.pop()//删后一
Array.shift()//删前一
//返回删除元素

Array.splice(3,2,1,2)//第四个开始删除两个，并在删除位置加入元素1和2，返回删除元素组成的数组

Array.slice()//接收 2 个输入参数：第一个是开始提取元素的索引，第二个是提取元素的结束位置索引(不包括结束位置元素)

Array.indexOf()//返回参数所在数组中的索引
```

2.键值对添加到对象中

```JS
const tekkenCharacter = {
  player: 'Hwoarang',
  fightingStyle: 'Tae Kwon Doe',
  human: true
};
rekkenCharacter.origin='South Korea';//1
const hair='hair color';
tekkenChharater[hair]='dyed orange';//2
```

3.操作对象属性

```JS
//删除
delete people.name

//检查是否存在
users.hasOwnProperty('Alan');
'Alan' in users;
//如果有"Alan"返回True

//Object,kays()
//将对象作为参数并返回代表对象中每个属性的字符串数组,数组中元素的顺序是不确定的。
```

