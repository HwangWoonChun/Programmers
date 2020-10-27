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

## 2. 전 https://programmers.co.kr/learn/courses/30/lessons/42577

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
## 3. 위장 https://programmers.co.kr/learn/courses/30/lessons/42578

* 해쉬 + 경우의 수

    * 동시에 일어나는 경우는 곱의 법칙을 사용
    
    * [[yellow_hat, headgear], [blue_sunglasses, eyewear], [green_turban, headgear]]
    
    * 중복인 헤드기어만 따져 보자
    
        * (headgear의 yellow_hat을 입을 경우 + headgear의 green_turban을 입을 경우 + 둘다 안입을 경우) * ..... -1(아무 것도 안입은 경우)

    ```swift
    let clothes: [[String]] = [["yellow_hat", "headgear"], ["blue_sunglasses", "eyewear"], ["green_turban", "headgear"]]
    //let clothes = [["crow_mask", "face"], ["blue_sunglasses", "face"], ["smoky_makeup", "face"]]
    print(solution(clothes))

    func solution(_ clothes:[[String]]) -> Int {

        var tempDict: [String: Int] = [:]

        for cloth in clothes {
            if let count = tempDict[cloth[1]] {
                tempDict[cloth[1]] = count + 1
            } else{
                tempDict[cloth[1]] = 1
            }
        }

        var count = 1
        for temp in tempDict {
            count *= (temp.value + 1)
        }
        count -= 1
        return count
    }
    ```
