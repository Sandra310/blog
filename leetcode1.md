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


196 ms
```
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    let result = new ListNode(0)
    let head = result
    let up = 0
    while(l1 || l2){
        let sum = (l1 ? l1.val: 0) + (l2 ? l2.val: 0) + up
        up = Math.floor(sum / 10)
        head.next = new ListNode(sum % 10)
        head = head.next
        if (l1) {
          l1 = l1.next
        }
        if (l2) {
          l2 = l2.next
        }
    }
    if (up > 0) {
        head.next = new ListNode(1)
    }
    return result.next
};
```

### 3、无重复字符的最长子串
```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

160ms
```
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    let array = []
    let maxlength = 0
    for(let i=0, len = s.length; i<len; i++){
        let index = array.indexOf(s[i])
        if (index >= 0) {
            array = array.splice(array.indexOf(s[i]) + 1)
        }
        array.push(s[i])
        maxlength = Math.max(maxlength, array.length)
    }
    return maxlength
};
```

### 4、寻找两个有序数组的中位数

```
给定两个大小为 m 和 n 的有序数组 nums1 和 nums2
请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。
你可以假设 nums1 和 nums2 不会同时为空

示例1：
nums1 = [1, 3]
nums2 = [2]
则中位数是 2.0

示例2：
nums1 = [1, 2]
nums2 = [3, 4]
则中位数是 (2 + 3)/2 = 2.5
```

236ms
```
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findMedianSortedArrays = function(nums1, nums2) {
    let array = nums1.concat(nums2)
    array = array.sort(function(a, b){
      return a - b
    })
    return (array.length % 2 == 0) ? (array[array.length / 2] + array[array.length / 2 - 1]) / 2  : array[Math.floor(array.length / 2)]
};
```

### 5、最长回文子串

```
给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000

输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案

输入: "cbbd"
输出: "bb"
```
