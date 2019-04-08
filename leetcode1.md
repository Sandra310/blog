## 1-10
### 1、两数之和

给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]

#### 常规 220ms
```
var twoSum = function(nums, target) {
    for(let i=0, len=nums.length; i<len; i++){
        let temp = nums.indexOf(target - nums[i])
        if (temp >= 0 && temp != i) {
            return [i, temp]
        }
    }
};
```
#### 比较好的 92ms
```
var twoSum = function(nums, target)  {
    let obj = {}
    for (let i = 0; i < nums.length; i++) {
        if (obj[nums[i]] !== undefined) {
            return [obj[nums[i]], i];
        } else {
            obj[(target - nums[i])] = i
        }
    }
};
```
```
var twoSum = function(nums, target) {
  const hm = new Map()
  for (let i = 0; i <= nums.length; i++){
    let z = target - nums[i]
    if (hm.has(z)) {
        return [hm.get(z), i]
    }
    hm.set(nums[i], i)
  }
};
```
第一种相当于两层循环，而下面的组装了个键值对，（差：原下标），一层循环就可以

### 2、两数相加

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807



