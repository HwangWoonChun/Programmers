# Programmers

## 1. 완주하지 못한 선수 https://programmers.co.kr/learn/courses/30/lessons/42576

* 해쉬 이용 

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

## 2. 완주하지 못한 선수 https://programmers.co.kr/learn/courses/30/lessons/42577

* 해쉬 이용하라고 되어 있으나, 이게 더 쉬워보여 적용

    * 각 전화번호 부의 첫번째 스트링만 필터한다.

    * 필터된 배열을 중복을 제거한다.
    
    * 필터된 배열과 기존 전화번호부의 크기를 비교 하여 다르면 false 반환

        ```swift
        //let phoneBook: [String] = ["119", "97674223", "1195524421"]
        //let phoneBook: [String] = ["123","456","789"]
        let phoneBook: [String] = ["12","123","1235","567","88"]
        print(solution(phoneBook: phoneBook))

        func solution(phoneBook: [String]) -> Bool {

            //폰북 길이 제한
            if phoneBook.count == 0 {
                print("error")
                return false
            }
            //각전화번호 길이 제한
            for phone in phoneBook {
                if phone.count > 20 {
                    print("error")
                    return false
                }
            }

            let filtered = phoneBook.map { $0.first }
            let set = Set(filtered)
            let duplicationRemovedArray = Array(set)
            if duplicationRemovedArray.count != phoneBook.count {
                return false
            } else {
                return true
            }
        }
        ```
