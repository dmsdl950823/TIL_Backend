# LeetCode 풀이

## Palidrome (Easy)

``` js
/**
 * @param {number} x
 * @return {boolean}
 */
const isPalindrome = function(x) {
    
  const reversed = String(x).split('').reverse().join('')
  const regex = new RegExp(reversed, 'g')

  return regex.test(x) 
}
```

## Palidrome Linked List (Easy)