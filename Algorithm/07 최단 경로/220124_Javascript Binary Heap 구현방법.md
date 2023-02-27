- [Javascript 이진 힙 (Binary Heap) 구현방법](#javascript-이진-힙-binary-heap-구현방법)
  - [최소 힙 Min Heap 코드로 구현하기](#최소-힙-min-heap-코드로-구현하기)
    - [삽입](#삽입)
    - [삭제](#삭제)

# Javascript 이진 힙 (Binary Heap) 구현방법

출처 :: [devgenius.io](https://blog.devgenius.io/how-to-implement-a-binary-heap-javascript-d3a0c54112fa)

*이진 힙 (Binary Heap)* 은 구현하기 복잡하지만, 다양한 곳에서 사용됩니다.

- 그래프 순회
- 정렬
- 길찾기

예를들어, Google Maps 은 A 부터 B 까지 가는 가장 빠른 길을 찾기 위해 일종의 이진 힙을 사용합니다. 

--- 

<img src="https://miro.medium.com/max/1400/1*N-T7axk-IX3IgZ-BewZGlQ.jpeg">

이진 힙을 사용하기 위해서는 쌓여있는 귤을 생각해보면 좋습니다.

쌓여있는 귤에서 하나를 뺄 때, **1. 가장 아래에 있는 귤을 빼면 귤 뭉치가 붕괴되며**, **가장 위에있는 귤이 가치있어보이기 때문에**  가장 높은곳에 있는 귤을 빼야합니다. 과일 뭉치의 아랫쪽에 위치하는 귤은 **우선순위에서 낮습니다.**

이진 힙에서도 똑같은 원리가 적용됩니다. 

<img src="../images/220124_이진힙.PNG">

이진 힙은 숫자, 글자, 오브젝트 등을 가지는 node 로 구성되어있습니다. 각 노드는 최대 2 개의 자식노드를 가지고 있습니다. (그래서 이름이 "이진 힙" 입니다)

힙의 가장 상위의 요소에서만 요소를 꺼낼 수 있는데, 그 노드가 **우선순위를 가지는** 노드입니다.

* **최대 힙** Max Heap :: 모든 부모노드가 자식 노드보다 더 크거나 같은 것
* **최소 힙** Min Heap :: 모든 부모노드가 자식 노드보다 더 작거나 같은 것

또한 이진 힙은 **항상 이진 트리 형태**여야합니다. 


-----

코드로 구현하기 전에 이해해야할 것은 트리가 어떻게 배열형식으로 구현되는지를 이해해야합니다.

* 트리의 루트노드는 배열의 1 번째에 위치합니다.
* 특정 노드(n)의 좌측 노드는 `2n` 에 위치해 있습니다.
* 특정 노드(n)의 우측 노드는 `2n + 1` 에 위치해 있습니다.
* 특정 노드(n)의 부모 노드는 `n / 2` 에 위치해 있습니다.

------

## 최소 힙 Min Heap 코드로 구현하기

``` js
export class MinHeap {
  constructor (selector) {
    this.items = []
    this.selector = selector
  }

  push () {}

  pop () {}
}
```

코드에서 `selector` 는 힙에 저장된 각 요소의 값을 리턴해주는, 사용자에 의해 제공되는 함수입니다. 저장된 요소/오브젝트와 비교하기 위해 사용됩니다.

### 삽입

힙에서, 각 요소는 완벽한 이진 트리 형식으로 구성되어 삽입됩니다. 새로운 요소를 배열에 추가하면 됩니다.

그런 다음, 노드를 "버블링" Bubble Up 하도록 합니다. 이것은 간단하게 부모 노드가 새롭게 삽입된 노드보다 작거나 같으면 둘을 바꾸는 것입니다.

``` js
export class MinHeap {
  constructor (selector) {
    this.items = []
    this.selector = selector
  }

  insert () {
    let i = this.items.length
    this.items.push(item)
    let parentIndex = Math.floor((i + 1) / 2 - 1)

    if (parentIndex < 0) parentIndex = 0

    let parentVal = this.selector(this.items[parentIndex])
    const pushedVal = this.selector(this.items[i])

    while (i > 0 && parentVal > pushedVal) {
      parentIndex = Math.floor((i + 1) / 2 - 1)
      this.swap(i, parentIndex)
      i = parentIndex
      parentVal = this.selector(
        this.items[Math.max(Math.floor((i + 1) / 2 - 1), 0)]
      )
    }
  }
}
```


### 삭제

힙에서 요소를 삭제하는 방법은 삭제 후 힙을 조정하는 것입니다. 그를 위해서는, 1. 완벽한 이진트리 형식을 유지해야합니다. 2. 타당힌 최소 힙 형태를 유지해야합니다.

이것은 힙의 마지막 요소(가장 큰 요소)가 가장 루트노드에 위치하게 하면서, \
최소 힙을 유지하기 위해 위에서 아래로 "버블링" Bubble Down 하도록 합니다.

``` js
export class MinHeap {
  constructor (selector) {
    this.items = []
    this.selector = selector
  }

  remove () {
    if (this.items.length <= 1) return this.items.pop()

    const ret = this.items[0]
    let temp = this.items.pop()

    this.items[0] = temp

    let i = 0 // top 에서 down 으로 heap을 조정
    while (true) {
      let rightChildIndex = (i + 1) * 2
      let leftChildIndex = (i + 1) * 2 - 1

      let lowest = rightChildIndex

      if (
        leftChildIndex >= this.items.length &&
        rightChildIndex >= this.items.length
      ) break
      
      if (leftChildIndex >= this.items.length) lowest = rightChildIndex
      if (rightChildIndex >= this.items.length) lowest = leftChildIndex

      // 가장 작은 자식 찾기
      if (
        !(leftChildIndex >= this.items.length) &&
        !(rightChildIndex >= this.items.length)
      ) {
        lowest = this.selector(this.items[rightChildIndex]) < this.selector(this.items[leftChildIndex]) ? rightChildIndex : leftChildIndex
      }

      // 만약 부모가 자식보다 더 큰 경우 (swap)
      if (this.selector(this.items[i]) > this.selector(this.items[lowest])) {
        this.swap(i, lowest)
        i = lowest
      } else {
        break
      }

      // 가장 상단의 요소를 리턴
      return ret
    }
  }
}
```


