# LeetCode 풀이

## Two Sums (Easy)

코테준비를 위해 풀이를 시작했다.

``` js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
	let test = []
	const queue = [...nums]
	let firstIdx = 0

	while (queue.length > 1) {

		for (let i = firstIdx; i < nums.length; i++) {
			if (i === firstIdx) continue
			// console.log(nums[firstIdx], nums[i])
			if (nums[firstIdx] + nums[i] === target) test = [firstIdx, i]
		}

		if (test.length) break

		queue.shift()
		firstIdx += 1

	}

	return test

};
```

## Add Two Numbers (Medium)

> 테스트케이스 (실패건)
> * Input `[1,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,0,1]`, `[5,6,4]`
> * Output `[0,3,NaN,NaN,1]`
> * 결과 : Wrong Answer

테스트케이스중 실패한 건이 있었으나, \
`setReverseLink()` 함수는 1차 연결리스트로 재사용할만해서 가져왔다.

``` js
// 결과 Fail
var isPalindrome = function(l1, l2) {

	// 연결리스트 순회해서 값 가져오기
	const getValue = (head) => {
		const values = []
		let current_node = head

		while (current_node !== null) {
			values.push(current_node.val)
			current_node = current_node.next
		}

		return values
	}


	// 1차 연결리스트 생성
	const setReverseLink = (value) => {
		const array = String(value).split('')
		let next_node = null
		
		while (array.length) {
			const val = array.shift()
			const current_node = { val, next: next_node }
			next_node = current_node
		}

		return next_node
	} 


	const l1Val = getValue(l1).reverse().join('')
	const l2Val = getValue(l2).reverse().join('')

	const sum = l1Val + l2Val

	return setReverseLink(sum)
}
```


### 다른사람의 풀이

``` js
/**
 * @param {ListNode} head
 * @return {boolean}
 */
var isPalindrome = function(l1, l2) {
  let sum = 0
  let current = new ListNode(0) // 처음 기본 노드 세팅

  let result = current

  while (l1 || l2) {
    if (l1) {
      sum += l1.val  // 현재 값
      l1 = l1.next
    }

    if (l2) {
      sum += l2.val  // 현재 노드의 값끼리 합산
      l2 = l2.next
    }

    current.next = new ListNode(sum % 10) // 10 이상이라면 1의 자리 수 만 가져옴
    current = current.next


    sum = sum > 9 ? 1 : 0
  }

  return result
}
```

``` 
1)
  sum += l1.val + l2.val ▶ 0 + 2 + 5 = 7
  current.next = 7 % 10 = 7
  sum = 7 > 9 ▶ 0
2)
  sum += l1.val + l2.val ▶ 0 + 4 + 6 = 10
  current.next = 10 % 10 = 0
  sum = 10 > 9 ▶ 1
3)
  sum += l1.val + l2.val ▶ 1 + 3 + 4 = 8
  current.next = 10 % 8 = 8
  sum = 8 > 9 ▶ 0
```