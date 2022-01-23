# LeetCode 풀이

## Longest Substring Without Repeating Characters

### 다른사람의 풀이
``` js
/**
 * @param {string} s
 * @return {number}
 */
 var lengthOfLongestSubstring = function(s) {
    let max_len = 0
    let curr = 0
    let hash = {}

    if (s.length < 2) return s.length  // s의 갯수가 1 개일 경우
    
    for (let i = 0; i < s.length; i++) {
      if (hash[s[i]] === undefined) curr += 1
      else curr = Math.min(i - hash[s[i]], curr + 1)

      max_len = Math.max(max_len, curr)
      hash[s[i]] = i // save the index
    }

    max_len

    return max_len
}


lengthOfLongestSubstring('pwwkew')

/*

ex1) 'pwwkew'
s[i]       // p, w, w, k, e, w
hash[s[i]] // undefined, undefined, 1, undefined, undefined, undefined, 2

curr = Math.min(i - hash[s[i]], curr + 1) ▶ min(2 - 1, 2 + 1) ▶ 1
curr = Math.min(i - hash[s[i]], curr + 1) ▶ min(5 - 2, 3 + 1) ▶ 3

max_len = Math.max(max_len, curr) ▶ max(0, 1) ▶ 1
max_len = Math.max(max_len, curr) ▶ max(0, 3) ▶ 3

*/
```