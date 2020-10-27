# Programmers

## 1. 완주하지 못한 선수 https://programmers.co.kr/learn/courses/30/lessons/42576

```swift
//["marina", "josipa", "nikola", "vinko", "filipa"]
//["josipa", "filipa", "marina", "nikola"]
let string = solution(participant: ["marina", "josipa", "nikola", "vinko", "filipa", "marina"], completion: ["josipa", "filipa", "marina", "nikola"])
print(string)

func solution(participant: [String], completion: [String]) -> [String] {
    var temp: [String:Int] = [:]
    
    for person in participant {
        temp[person] = 0
    }

    var returnArr: [String] = []
    for person in participant {
        if completion.contains(person) {
            let count = temp[person] ?? 0
            temp[person] = count + 1
        }
        if temp[person] ?? 0 == 0 || temp[person] ?? 0 > 1 {
            returnArr.append(person)
        }
    }

    return returnArr
}
```
