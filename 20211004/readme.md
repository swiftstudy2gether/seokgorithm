# 럭키 스트레이트

```swift
import Foundation

let a = readLine()

if let a = a{
    var num = Int(a)!
    let half = a.count / 2
    var suffix = 0
    var prefix = 0
    var cnt = 0

    while num > 0{
        if cnt < half{
            suffix += num % 10
            num /= 10
            cnt += 1
        }else{
            prefix += num % 10
            num /= 10
            cnt += 1
        }
    }
    let ret = prefix == suffix ? "LUCKY" : "READY"
    print(ret)
}
```



# 문자열 재정렬

```swift
import Foundation

let a = readLine()

if let a = a{
    var a = Array(a)
    a = a.sorted(by: <)
    var num = 0
    var str = ""
    for i in 0..<a.count{
        if a[i].isNumber{
           num += Int(String(a[i]))!
        }else if a[i].isLetter{
            str += String(a[i])
        }
    }
    print("\(str)\(num)")
}

```



# 문자열 압축

```swift
import Foundation

func solution(_ s:String) -> Int {

    var retArr = [Int]()
    var cutWordCnt = 0

    while cutWordCnt <= s.count / 2{
        var wordCnt = 1
        var index = 0
        var ansWord = ""
        var pre = ""
        cutWordCnt += 1

        while index <= s.count{
            let remainder = s.suffix(s.count - index)
            let prefixWord = remainder.prefix(cutWordCnt)
            if pre ==  prefixWord{
                wordCnt += 1
                index += cutWordCnt
                continue
            }
            if wordCnt > 1{
                ansWord += "\(wordCnt)\(pre)"

            }else{
                ansWord += pre
            }
            pre = String(prefixWord)
            wordCnt = 1
            index += cutWordCnt
        }
        ansWord += s.suffix(s.count - (index - cutWordCnt))
        retArr.append(ansWord.count)
    }
    return retArr.min()!
}

```

