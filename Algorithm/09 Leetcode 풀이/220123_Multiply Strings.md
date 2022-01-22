# LeetCode 풀이

## Multiply Strings (Medium)

> 테스트케이스 (실패건)
> * Input `9`, `99`
> * Output `811`
> * Expected `891`
> * 결과 : Wrong Answer

마지막에 나오는 결과가 10 이상인 경우를 어떻게 처리해야할지 몰라서 실패했다.

``` js
/**
 * @param {string} num1
 * @param {string} num2
 * @return {string}
 */
 var multiply = function(num1, num2) {
    const number1 = num1.split('')
    const number2 = num2.split('')

    let loopCount = 0
    const allSum = []

    // 987654321 기준 => 전체 곱하기 만들기
    for (let i = number2.length - 1; i > -1 ; i--) {
      let sum = 0
      const add = []

      for (let j = number1.length - 1; j > -1; j--) {
        // console.log(number1[j])
        const one = Number(number1[j])
        const two = Number(number2[i])
        const multiply = (one * two) + sum
        let push = 0
        
        // console.log(`${one} * ${two} = ${one * two} + ${sum} => ${multiply}`)
        
        
        // 곱했는데 10 이상인 경우
        if (multiply > 9) {
          const tempSum = String((multiply)).split('')
          sum = Number(tempSum.shift())
          push = Number(tempSum[0])

          if (j === 0 && i === 0) { // 마지막에 도달했으나 10 이상인 경우 (ㅠㅠ 실패)
            // multiply
            // sum
            sum = 0
            add.splice(0, 0, multiply + sum)
            break
          }

        } else {
          sum = 0
          push = multiply
        }

        add.splice(0, 0, push)
      }

      for (let cnt = 0; cnt < loopCount; cnt++) add.splice(add.length, 0, 0)
      loopCount += 1
      // console.log(number2[i], add)
      allSum.push(add)
    }

    console.log(allSum)
    let sumCnt = allSum[allSum.length - 1].length
    let upper = 0
    const result = []

    while (sumCnt > 0) {
      let sum = 0 + upper

      const temp = [] // 💕
      for (let i = 0; i < allSum.length; i++) {
        const last = allSum[i].pop() || 0
        temp.push(last) // 💕
        sum += last
      }

      // console.log(temp, sum)
      if (sumCnt === 1) {
        result.splice(0, 0, sum)
        break
      }

      if (sum > 9) {
        const total = String(sum).split('')
        result.splice(0, 0, total.pop())
        upper = Number(total.join(''))
      } else {
        result.splice(0,0, sum)
        upper = 0
      }

      sumCnt -= 1
    }

    console.log(result.join(''))
    return result.join('')
}

// multiply('123456789', '987654321')
// multiply('123', '456')
multiply('9', '99')
```

### 다른사람의 풀이

``` js
/**
 * @param {string} num1
 * @param {string} num2
 * @return {string}
 */
var multiply = function(num1, num2) {    
    if (num1 === "0" || num2 === "0") {
        return "0"
    }
        
    let firstNumber = [...num1]
    let secondNumber = [...num2]
    
    // Reverse both the numbers.
    firstNumber.reverse()
    secondNumber.reverse()

    // To store the multiplication result of each digit of secondNumber with firstNumber.
    let N = firstNumber.length + secondNumber.length
    let answer = new Array(N).fill(0)
        
    for (let place2 = 0; place2 < secondNumber.length; place2++) {
        let digit2 = Number(secondNumber[place2])

        // For each digit in secondNumber multiply the digit by all digits in firstNumber.
        for (let place1 = 0; place1 < firstNumber.length; place1++) {
            let digit1 = Number(firstNumber[place1])

            // The number of zeros from multiplying to digits depends on the 
            // place of digit2 in secondNumber and the place of the digit1 in firstNumber.
            let currentPos = place1 + place2

            // The digit currently at position currentPos in the answer string
            // is carried over and summed with the current result.
            let carry = answer[currentPos]
            let multiplication = digit1 * digit2 + carry

            // Set the ones place of the multiplication result.
            answer[currentPos] = multiplication % 10

            // Carry the tens place of the multiplication result by 
            // adding it to the next position in the answer array.
            answer[currentPos + 1] += Math.floor(multiplication / 10);
        }
    }

    if (answer[answer.length - 1] == 0) {
        answer.pop()
    }

    // Ans is in the reversed order.
    // Reverse it to get the final ans.
    answer.reverse()
    return answer.join('')
}
```