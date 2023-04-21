# 找到字符串中所有字母异位词

> 难度：中等
>
> 次数：1
>
> https://leetcode.cn/problems/find-all-anagrams-in-a-string

## 题目

给定两个字符串`s`和`p`，找到`s`中所有`p`的**异位词**的子串，返回这些子串的起始索引。不考虑答案输出的顺序。

**异位词**指由相同字母重排列形成的字符串（包括相同的字符串）。

### 示例

#### 示例 1：

```
输入: s = "cbaebabacd", p = "abc"
输出: [0,6]
解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的异位词。
```

#### 示例 2：

```
输入: s = "abab", p = "ab"
输出: [0,1,2]
解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的异位词。
```

## 解法

### 滑动窗口+哈希表

```javascript
/**
 * @param {string} s
 * @param {string} p
 * @return {number[]}
 */
const findAnagrams = function (s, p) {
  const pCount = new Array(26).fill(0)
  const base = 'a'.charCodeAt()
  const ans = []

  for (let i = 0; i < p.length; i++) {
    pCount[p[i].charCodeAt() - base]++
  }

  const sCount = new Array(26).fill(0)
  let left = 0
  let right = 0

  while (right < s.length) {
    const rightChar = s[right].charCodeAt() - base
    sCount[rightChar]++
    right++

    while (sCount[rightChar] > pCount[rightChar]) {
      const leftChar = s[left].charCodeAt() - base
      sCount[leftChar]--
      left++
    }

    if (right - left === p.length) {
      ans.push(left)
    }
  }

  return ans
}
```