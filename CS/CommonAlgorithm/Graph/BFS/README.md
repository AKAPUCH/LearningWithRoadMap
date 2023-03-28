# 그래프의 너비 우선 탐색(BFS)

- 그래프의 순회중 정점의 이웃 정점들을 먼저 방문하는 방법
- 방향 유형에 관계없이 사용가능
- queue 자료구조를 사용합니다.
## 알고리즘 로직
	큐에 넣는 것은 다음 순서에 해당 정점을 방문하겠다는 의미입니다
	큐에서 빼는 것은 해당 정점을 현재 시점에 방문했다는 의미입니다
	대기열에 존재하는 정점이 없으면 종료합니다
1. 정점을 방문하는 것을 표현하기 위한 대기열(queue)를 선언합니다.
2. 출발 정점을 대기열에 추가합니다. 
3. 대기열에서 꺼낸 정점을 저장할 순서가 보장되는 컬렉션 자료구조를 선언합니다.(주로 배열)
4. 대기열의 첫번째 정점을 빼내서 배열에 저장하고 그 정점의 이웃 정점들을 대기열에 추가합니다.
5. 4번 과정을 계속 반복합니다. 대기열에 남아있는 정점이 없다면 탐색을 종료합니다.
6. 배열 끝에 정점을 append()하는 식으로 저장했다면 정점을 방문한 순서를 알 수 있습니다. 
## 활용 1 : [백준 2606번 바이러스](https://www.acmicpc.net/problem/2606)

<details>
<summary>구현 코드</summary>

```swift
let v = Int(readLine()!)!
let e = Int(readLine()!)!
var cnt = 0
var vertexArr : [[Int]] = Array(repeating : [], count : v+1)
for _ in 0..<e {
  let edge = readLine()!.split(separator: " ").map{Int(String($0))!}
  vertexArr[edge[0]].append(edge[1]) // 간선을 저장
  vertexArr[edge[1]].append(edge[0]) // 무방향이므로 반대방향도 넣기
}
var visitCheckArr : [Bool] = Array(repeating: false, count: v+1)
var queue : [Int] = []
queue.append(1)
visitCheckArr[1] = true
while !queue.isEmpty {
  let visitVertex = queue.removeFirst()
  for neighborVertex in vertexArr[visitVertex] {
    if visitCheckArr[neighborVertex] {continue}
    visitCheckArr[neighborVertex] = true
    cnt += 1
    queue.append(neighborVertex)
  }
}

print(cnt)
```
</details>
