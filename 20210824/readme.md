# Programmers.로또의 최고 순위와 최저 순위

## 문제 설명

> lottos와 win_nums 2개의 배열이 들어온다.
>
> lottos는 내가 산 로또 번호
>
> win_nums 는 금주의 로또 번호이다. 
>
> 동생이 낙서를 하여 로또 번호가 훼손이 되어서 훼손된 부분은 0으로 입력하였다.
>
> 당첨될수 있는 최고의 순위와 최저의 순위를 배열에 담아서 반환하면 된다.

## 문제 풀이

```swift
import Foundation

func solution(_ lottos:[Int], _ win_nums:[Int]) -> [Int] {

    var rightCount:Int = 0
    var answer:[Int] = []
    var zeroCount:Int = 0
    for i in 0..<win_nums.count{
        for j in 0..<lottos.count{
            if win_nums[i] == lottos[j]{
                rightCount += 1
            }
        }
        if lottos[i] == 0{
            zeroCount += 1
        }
    }
    answer.append(7 - (zeroCount + rightCount))
    answer.append(7 - rightCount)
    if answer[0] == 7{
        answer[0] = 6
    }
    if answer[1] > 6{
        answer[1] = 6
    }
    return answer
}
```

## 힘들었던 점

> 이번 문제는 정답 로또에서 내 로또 번호와 비교하여 로또번호가 맞으면 rightCount 를 1 올려주고 0이라면 zeroCount를 1 올려준다.
>
> 만약 하나도 못맞쳤다면 7이 나올 수 있는데 그럴 경우에는 낙첨인 6등이기 때문에 7이상의 값은 6으로 수정한다.

## [문제 바로가기](https://programmers.co.kr/learn/courses/30/lessons/77484)

# Programmers.신규 아이디 추천

## 문제 설명

> 주어진 단계를 차례차례 구현하면 되는 간단한 문제이다.

```
1단계 new_id의 모든 대문자를 대응되는 소문자로 치환합니다.
2단계 new_id에서 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.)를 제외한 모든 문자를 제거합니다.
3단계 new_id에서 마침표(.)가 2번 이상 연속된 부분을 하나의 마침표(.)로 치환합니다.
4단계 new_id에서 마침표(.)가 처음이나 끝에 위치한다면 제거합니다.
5단계 new_id가 빈 문자열이라면, new_id에 "a"를 대입합니다.
6단계 new_id의 길이가 16자 이상이면, new_id의 첫 15개의 문자를 제외한 나머지 문자들을 모두 제거합니다.
     만약 제거 후 마침표(.)가 new_id의 끝에 위치한다면 끝에 위치한 마침표(.) 문자를 제거합니다.
7단계 new_id의 길이가 2자 이하라면, new_id의 마지막 문자를 new_id의 길이가 3이 될 때까지 반복해서 끝에 붙입니다.
```

## 문제 풀이

```swift
import Foundation

func solution(_ new_id:String) -> String {
    var id:String = new_id

    //1단계
    id = id.lowercased()

    //2단계
    var tmp_id:String = ""
    for i in id{
        if i.isLowercase || i.isNumber || i == "-" || i == "_" || i == "."{
            tmp_id.append(i)
        }
    }

    //3단계
    while tmp_id.contains(".."){
        tmp_id = tmp_id.replacingOccurrences(of: "..", with: ".")
    }

    //4단계
    if tmp_id.hasPrefix("."){
        tmp_id.removeFirst()
    }
    if tmp_id.hasSuffix("."){
        tmp_id.removeLast()
    }

    //5단계
    if tmp_id == ""{
        tmp_id.append("a")
    }

    //6단계
    if tmp_id.count >= 16{
        let last = tmp_id.index(tmp_id.startIndex, offsetBy: 15)
        tmp_id = String(tmp_id[tmp_id.startIndex..<last])
        if tmp_id.hasSuffix("."){
            tmp_id.removeLast()
        }
    }

    //7단계
    if tmp_id.count <= 2 {
        while tmp_id.count != 3 {
            tmp_id = tmp_id + String(tmp_id.last!)
        }
    }
    return tmp_id
}
```

## 힘들었던 점

> 6단계에서 특정 인덱스를 탐색하는 법을 잘 몰라서 엄청 시간을 잡아먹었다.
>
> 구글에 있는 [블로그](http://seorenn.blogspot.com/2018/05/swift-string-index.html)를 보고 간신히 구현에 성공했다.
>
> 그리고 저번에 배운 replacingOccurrences 함수가 문제 푸는데 많은 도움이 되었다. 

## [문제 바로가기](https://programmers.co.kr/learn/courses/30/lessons/72410)

