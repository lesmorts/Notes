- 生成范围内的随机整数

  ```JS
  function randomRange(myMin, myMax) {
    return Math.floor(Math.random()*(myMax-myMin+1))+myMin;
  }
  ```

  

- 用递归生成倒计时

  ```JS
  function countdown(n) {
    if (n<1) {
      return [];
    } else {
      const countArray = countdown(n-1);
      countArray.unshift(n);
      return countArray;
    }
  }
  //在unshift n 之前，先生成[] 再逐步填入1,2,3,4...n-1
  ```
  
  
  
- 递归插入数组

  ```JS
  function rangeOfNumbers(startNum, endNum) {
    if (startNum == endNum)
      return [startNum];
    else{
      const arr=rangeOfNumbers(startNum,endNum-1);
      arr.push(endNum);
      return arr;
    }
  };
  ```
  
  