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

## Palidrome Linked List (Medium)

`head` 가 조건이 있는 연결리스트로 구현되어있어 일단 연결리스트부터 코드로 작성하였다.

### 직접 작성한 답안

``` js
/**
 * @param {ListNode} head
 * @return {boolean}
 */
 var isPalindrome = function(head) {
    const values = []
    const getAllVals = (node) => {
        values.push(node.val)
        if (node.next === null) return values
        else return getAllVals(node.next)
    }

    const value = getAllVals(head)

    const sorted = value.join('')
    const reversed = value.reverse().join('')
    const regex = new RegExp(sorted, 'g')
    // console.log(sorted, reversed, regex.test(reversed))
    return regex.test(reversed)
}

// ====
// ====
// ====

/**
 * Definition for singly-linked list.
 * 연결리스트 구현
 * function ListNode(val, next) {
 *     this.val = (val === undefined ? 0 : val)
 *     this.next = (next === undefined ? null : next)
 * }
 */
function ListNode(val, next) {
    this.val = (val === undefined ? 0 : val)
    this.next = (next === undefined ? null : next)
}

function setLinkedList (array) {
    let lastLinkedList = null
    while (array.length) {
        const last = array.pop()
        lastLinkedList = new ListNode(last, lastLinkedList)
    }
    return lastLinkedList
}

// const LinkedList = setLinkedList([1, 2, 2, 1])
const LinkedList = setLinkedList([1, 2, 3])


isPalindrome(LinkedList) // true
```

### 다른사람의 풀이

``` js
/**
 * @param {ListNode} head
 * @return {boolean}
 */
 var isPalindrome = function(head) {
    const values = []
    let current_node = head

    while (current_node !== null) {
        values.push(current_node.val)
        current_node = current_node.next
    }
    // console.log(values, values.reverse(), values === values.reverse())

    return values === values.reverse() 
}

// 연결리스트 구현은 생략
```