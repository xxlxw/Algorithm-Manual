# 两数之和

看到这个题第一反应就是双重循环，遍历出要求的结果。虽然也成功了，但是时间复杂度还是很高。之后就去看了解法，他们使用了哈希表来保存值，这样就将双重循环降成一遍了。

## 思路一：暴力求解

两个for循环，外循环为`for(let i=0,len=nums.length;i<len-1;i++)`,内循环为`for(let j=i+1;j<len;j++)`。需要注意两次循环的起始和终止条件，保证全部能遍历，且不会重复做无用功，这里使用`len`变量来保存`nums`的长度，略微优化一下运算速度。

## 思路二：单哈希表求解

正常的哈希表需要有个哈希算法来建立。在这里我们直接用js语言的特性，直接声明一个对象字面量，用`obj[expression]`的方式来存取键值，其中`value`为匹配条件的元素的数组下标。我们遍历数组，判断是否`[target-nums[i]]`元素是否存在，存在则说明满足条件，返回数组`[target-nums[i],i]`。不存在，则执行语句`obj[nums[i]]=i`。

这里需要注意的是，`if`的判断条件为`obj[target-nums[i]]!==undefined`，如果单纯的写成`if(obj[target-nums[i]])`则会存在bug：当值为0，应返回结果，这里却走了else的逻辑。

如：当前是`nums[0]=2`，取`obj[9-2=7]`不存在，为`undefined`，执行`obj[2]=0`;到了下一次循环`nums[1]=7`，取`obj[9-7=2]`值为`0`，存在，则返回结果`[0,1]`;
以下是实现代码：

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (nums, target) {
    let exist = {};
    for (let i = 0; i < nums.length; i++) {
        if (exist[target - nums[i]] !== undefined) {
            return [exist[target - nums[i]], i];
        }
        exist[nums[i]] = i;
    }
};
```
​	