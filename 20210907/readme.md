# Programmers.크레인 인형뽑기 게임

## 문제 설명

> board와 moves 의 인자가 들어온다.
>
> board 는 0이면 비어있는 칸 숫자면 인형이 들어있는 판이다.
>
> moves는 board를 가로로 몇칸 움직일지 정하는 인자이다.
>
> board의 행을 i 열을 j 로 가정한다면 
>
> moves는 가로로 움직이기 때문에 j 값에 영향을 받는다
>
> 그러므로 moves에 해당하는 열에 가서 i 값의 카운트를 늘려주면서 0이 아닌수가 나올때까지 검사를 한다.
>
> 0이 아닌 수를 arr에 값이 아무것도 없다면 그냥 넣는다.
>
> arr에 값이 있다면 arr의 마지막 원소와 현재 값과 비교를 하여 같다면 추가를 하지않고 arr 원소를 지우고 answer 를 +1 추가한다.
>
> 인형은 1개가 삭제된것이 아닌 1쌍 2개가 삭제된것이기때문에 마지막에 answer * 2를 해서 리턴 해주면 된다.

## 문제 풀이

```swift
import Foundation

func solution(_ board:[[Int]], _ moves:[Int]) -> Int {
    var board = board
    var answer:Int = 0
    var arr:[Int] = []

    for i in moves{
        for j in 0..<board.count{
            let target:Int = board[j][i-1]
            if target != 0{
                board[j][i-1] = 0
                if target == arr.last{
                    arr.removeLast()
                    answer += 1
                }else{
                    arr.append(target)
                }
                break
            }
        }
    }
    return answer * 2
}
```

## [문제 바로가기](https://programmers.co.kr/learn/courses/30/lessons/64061?language=swift)

# Programmers.음양 더하기

## 문제 설명

> absolutes 라는 숫자 인자와 signs 라는 bool 인자가 들어온다.
>
> signs 각각 인덱스와 absolutes 인덱스는 대칭으로 
>
> true 면 양수 false면 음수로 처리하여 각 숫자의 합을 반환한다.

## 문제 풀이

### 나의 풀이

 ```swift
 import Foundation
 
 func solution(_ absolutes:[Int], _ signs:[Bool]) -> Int {
     
     var answer:Int = 0
     for i in 0..<signs.count{
         if signs[i] == true{
             answer += absolutes[i]
         }else{
             answer -= absolutes[i]
         }
     }
     return answer
 }
 ```

### 다른 사람 풀이

```swift
import Foundation

func solution(_ absolutes:[Int], _ signs:[Bool]) -> Int {
    return (0..<absolutes.count).map{signs[$0] ? absolutes[$0] : -absolutes[$0]}.reduce(0, +)
}
```

## 힘들었던 점

> 문제는 쉽게 풀었었다..
>
> 스터디를 준비하면서 문제를 다시 보면서 map,reduce,fliter로 쉽게 구현할 수 있지 않을까 생각하면서 다시 문제를 풀려고했었다.
>
> map을 이용해 2개의 배열을 하나의  배열로 만들기 어려워서 다른 사람의 풀이를 보았다. 
>
> signs에 들어있는 값이 bool 값임을 이용해 삼항연산자를 사용한점과 map의 범위를 숫자로도 정할수 있는점이 참신하게 다가왔다.

## [문제 바로가기](https://programmers.co.kr/learn/courses/30/lessons/76501?language=swift)

# Programmers.실패율

## 문제 설명

> 실패율은 다음과 같이 정의한다.
>
> - 스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수 / 스테이지에 도달한 플레이어 수
>
> 전체 스테이지의 개수 N
>
> 게임을 이용하는 사용자가 현재 멈춰있는 스테이지의 번호가 담긴 배열 stages가 매개변수로 주어질 때
>
> 실패율이 높은 스테이지부터 내림차순으로 스테이지의 번호가 담겨있는 배열을 return 하도록 solution 함수를 완성하라.

## 문제 풀이

### 나의 풀이

```swift
import Foundation

func solution(_ N:Int, _ stages:[Int]) -> [Int] {

    var failure: [Int: Float] = [:]
    var player: Int = stages.count

    for i in 1...N {
        let n = stages.filter { $0 == i }.count
        failure[i] = Float(n)/Float(player)
        player -= n
    }

    return failure.sorted(by: <).sorted(by: { $0.value > $1.value }).map {$0.key}
}
```

> 테스트 5, 테스트 9, 테스트 22에서 시간 초과가 발생한다.

```swift
import Foundation

func solution(_ N:Int, _ stages:[Int]) -> [Int] {

    var failStage: [Int: Int] = [:]
    for stage in stages {
        if !failStage.isEmpty && failStage.keys.contains(stage) {
            failStage[stage]! += 1
            continue
            }
        failStage[stage] = 1
    }

    var result: [(stage: Int, value: Double)] = []
    var successPeople: Int = stages.count
    for stage in 1...N {
        if !failStage.keys.contains(stage) {
            result.append((stage, 0))
             continue
             }
        result.append((stage, Double(failStage[stage]!) / Double(successPeople)))

        successPeople -= failStage[stage]!
    }
    
    result.sort { return $0.value == $1.value ? $0.stage < $1.stage : $0.value > $1.value }
    return result.map { $0.stage }

}
```

> 정상적으로 채점 완료

## 힘들었던 점

> 시간 복잡도를 따지지 않고 문제를 풀다보니 
>
> 고차 함수가 느린 함수라는 점을 모르고 진행해서 시간초과가 난 점이다.
>
> 결국 인터넷에 다른사람의 블로그를 탐색하면서 틀린 이유를 찾았고 그 사람들의 코드를 보고 공부를 하면서 다시 코드를 짰다.

## [문제 바로가기](https://programmers.co.kr/learn/courses/30/lessons/42889?language=swift)

