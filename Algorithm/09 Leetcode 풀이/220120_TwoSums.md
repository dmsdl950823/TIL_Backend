# LeetCode 풀이

## Two Sums (Easy)

코테준비를 위해 풀이를 시작했다...

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

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcNpIpx%2FbtrrfJxq4qb%2FNgxjVfvV21sxtztBm9KJ2K%2Fimg.png">