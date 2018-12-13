# 概述
1. 2018.1017,https://css-tricks.com/why-using-reduce-to-sequentially-resolve-promises-works/
1. 异步处理可以使用https://github.com/caolan/async
1. 使用Array.prototype.reduce()是解决顺序promise的最推荐的解决办法
1. reduce是es5标准
1. 文章提供的reduce方法只是一种能。但基本不会有人使用的，用promise.all即可

## 读后总结

1. reduce不同于其他高级函数（map等），可以用于处理promise
2. 学习使用reduce的使用
3. 由于评论对此方法批评较多，而且reduce实现promise使用较为麻烦，未看完

## 什么是reducer
1. 总是返回1个值，这个值可以是string，number，array等任意类型

1. ```javascript
    const nums = [1, 3, 6]
    const reducer = (acc, item) => acc + item
    const total = nums.reduce(reducer, 0)
    ```

1. 开始acc=0，item=,1，返回值为1；然后第2次循环acc=1，item=3，返回值4；第3次循环acc=4，item=6，返回值10

# 基本用法举例

## 查找array数字出现的次数

```javascript
const nums = [3, 5, 6, 82, 1, 4, 3, 5, 82]
const result = nums.reduce((tally, amt) => {
  tally[amt] ? tally[amt]++ : tally[amt] = 1
  return tally
}, {})
```

## 将数组基于某些条件转换为对象

1. 如将数组中数转换为奇数和偶数版本

2. ```javascript
   const nums = [3, 5, 6, 82, 1, 4, 3, 5, 82]
   const result = nums.reduce((acc, item) => {
     acc[item] = {
       odd: item % 2 ? item : item - 1,
       even: item % 2 ? item + 1 : item
     }
     return acc
   }, {})
   console.log(result)
   ```



# 