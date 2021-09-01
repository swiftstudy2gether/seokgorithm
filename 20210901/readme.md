# Programmers.숫자 문자열과 영단어(swift)

## 문제 설명

> 문자열에 있는 영어로된 숫자를 진짜 숫자로 바꾸어서 Int 형으로 반환한다.

## 문제 풀이

### 나의 풀이

```swift
import Foundation

let number:Dictionary<String, String> = ["zero" : "0", "one" : "1", "two" : "2", "three" : "3", "four" : "4", "five" : "5", "six" : "6", "seven" : "7", "eight" : "8", "nine" : "9"]

func solution(_ s:String) -> Int {
    var answer:String = ""
    var word:String = ""
    for index in s.indices{
        if s[index] >= "0" && s[index] <= "9"{
            answer.append(s[index])
        }else{
            word.append(s[index])
            if number[word] != nil{
                answer.append(number[word]!)
                word = ""
            }
        }

    }
    return Int(answer)!
}
```

### 다른 사람의 풀이

```swift
import Foundation


func solution(_ s:String) -> Int {
    var answer:String = s
    answer = answer.replacingOccurrences(of: "zero", with: "0")
    answer = answer.replacingOccurrences(of: "one", with: "1")
    answer = answer.replacingOccurrences(of: "two", with: "2")
    answer = answer.replacingOccurrences(of: "three", with: "3")
    answer = answer.replacingOccurrences(of: "four", with: "4")
    answer = answer.replacingOccurrences(of: "five", with: "5")
    answer = answer.replacingOccurrences(of: "six", with: "6")
    answer = answer.replacingOccurrences(of: "seven", with: "7")
    answer = answer.replacingOccurrences(of: "eight", with: "8")
    answer = answer.replacingOccurrences(of: "nine", with: "9")
    return Int(answer)!
}
```

## 소 감

> 문제를 다 풀고 다른사람은 얼마나 참신하게 풀었을까 궁금함에 들어갔다가 후회했다..
>
> 함수 하나로 너무 쉽게 문제를 해결했다. 
>
> replacingOccurences 함수 꼭 기억해서 코딩테스트때 써먹자

## [문제 바로가기](https://programmers.co.kr/learn/courses/30/lessons/81301?language=swift)

# Programmers.키패드 누르기(Swift)

## 문제설명

> 1, 4, 7은 왼손
>
> 3, 6, 9는 오른손
>
> 2, 5, 8, 0 은 왼손 오른손중 더 가까운 손이 간다.

## 문제 풀이

```swift
import Foundation

//목표 번호와 현재 손위치의 거리 계산
func handDistance(_ cur:[Int], _ target:[Int]) -> Int{
    return abs(target[0] - cur[0]) + abs(target[1] - cur[1])
}

func solution(_ numbers:[Int], _ hand:String) -> String {
    var answer:String = ""
    
    var leftHand:[Int] = [4,1]
    var rightHand:[Int] = [4,3]
    
    for var number in numbers{
        if number == 0{
            number = 11
        }
        switch number {
        case 1, 4, 7:
            answer += "L"
            leftHand = [(number / 3) + 1, 1]
        case 3, 6, 9:
            answer += "R"
            rightHand = [(number / 3), 3]
        default:
            let row:Int = (number / 3) + 1
            let numPos = [row , 2]
            let leftHandDist:Int = handDistance(leftHand, numPos)
            let rightHandDist:Int = handDistance(rightHand, numPos)
            
            if leftHandDist < rightHandDist{
                answer += "L"
                leftHand = numPos
            }else if leftHandDist > rightHandDist{
                answer += "R"
                rightHand = numPos
            }else{
                if hand == "left"{
                    answer += "L"
                    leftHand = numPos
                }else{
                    answer += "R"
                    rightHand = numPos
                }
            }
        }
    }
    return answer
}
```

## 소 감

> 0을 10으로 치환해서 각각 줄마다 3의 차이가 나는것을 이용해 % 계산을 통해 현재 자리를 구하는 점이 참신했다. 

## [문제 바로가기](https://programmers.co.kr/learn/courses/30/lessons/67256?language=swift)
