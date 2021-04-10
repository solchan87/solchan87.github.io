# Swift 문법
> 2018.01.22 업데이트    

## Collection Type
* Swift는 값의 모음을 저장하기위한 `Array`(배열), `Set`(집합), `Dictionary`(사전)이라는 세가지 기본 형식을 제공한다.  
* `Array`(배열)는 정렬된 값의 모음이며, 배열은 Index값을 가지고 있다.   
* `Set`(집합)은 고유 한 값의 정렬되지 않은 모음이며, 두개의 집할을 비교하여 값을 얻을 수 있다.   
* `Dictionary`(사전)는 키-값의 정렬되지 않은 모음이며, 키의 매칭을 통해 값을 찾을 수 있기 때문에 키는 중복될 수 없다.   

### Mutability of Collections
* Collection을 `var`에 할당하면 추가, 제거 수정등 변경이 가능하다.   
* 하지만, `let`에 할당하면 Collection을 변경할 수 없다.   

## Array
* 배열(Array)은 번호(Index)와 번호에 대응하는 데이터(Value)들로 이루어진 자료 구조를 나타낸다.   
* 일반적으로 배열에는 같은 종류의 데이터들이 순차적으로 저장되며, 값(Value)의 번호(Index)가 곧 배열의 시작점으로부터 상대적인 위치로 저장된다.   

### Array 문법
* 기본 표현은 Array<Element>로 Array Type을 나타낸다.  
```swift
// 빈 배열은 타입을 추론할 수 없기 때문에 좌변에서 타입 선언을 해야 한다.
// 여기에서 Element는 배열에 저장할수 있는 타입이다.
var arr1 = Array<Element>()
var arr2: Array<Element> = Array()
var arr3 = [Element]()
var arr4: [Element] = []

// Array 리터럴
var someInts:[Int] = [1,2,3,4]
someInts = []

// 시퀀스
let arr7 = Array(1...5) // CountableClosedRange<Int> : Sequence
let chars = Array("hello world".characters)
```

### 배열의 추가 기능
```swift
//배열의 Element 갯수
someInts.count

//빈 배열 확인
someInts.isEmpty // false
emptyArray.isEmpty //true

//Element 추가
someInts.append(5) // [1, 2, 3, 4, 5]

//Element 삽입
someInts.insert(0, at: 3) // [1, 2, 3, 0, 4, 5]

//Element 삭제
someInts.remove(at: 3)
print(someInts) // [1, 2, 3, 4, 5]
```

## Set
* Set은 같은 타입의 데이터가 순서없이 모여있는 자료구조,  각 항목의 순서가 중요치 않거나 한번만 표시해야하는 경우 배열대신 사용된다.   

### Set 문법
* 기본 표현은 Set<Element>로 Set Type을 나타낸다.   
* 여기에서 Element는 배열에 저장할수 있는 타입이다.   
* Set은 Array와 다르게 축약 문법이 없다.  

```swift
var someInts:Set<Int> = Set<Int>()
``` 

```swift
// Set 문법 예제
func setTest(){
    let oddDigits: Set = [1, 3, 5, 7, 9]
    let evenDigits: Set = [2, 4, 6, 8]
    let primeDigits: Set = [2, 3, 5, 7]
    
    print("test=========")
    // 교집합
    let intersectList = oddDigits.intersection(evenDigits)
    print(intersectList)
    
    let differenceList = oddDigits.symmetricDifference(primeDigits)
    print(differenceList)
    
    let unionList = oddDigits.union(evenDigits).sorted()
    print(unionList)
    
    let subtractList = oddDigits.subtracting(primeDigits).sorted()
    print(subtractList)
}

setTest()
```

## Dictionary
* Dictionary는 순서가 정해져 있지 않은 데이터에 키값을 통해 구분할수 있는 자료구조다.   
* 항목의 순서가 중요치 않고 key값을 통해서 데이터를 접근한다.  

### Dictionary 문법
* 기본 표현은 Dictionary<key, value>로 Dictionary Type을 나타낸다.  
* Key값 은 Dictionary에서 value를 가져오는데 사용되는 값이다.   
* 또 다른 축약 문법으로 [key:value] 로 표현할 수 있다.   

```swift
var someInts:[String:Int] = [String:Int]() 
var someInts:Dictionary<String,Int> = [:]

// Dictionary 리터럴
var airports: [String:String] = ["ICH": "인천공항", "CJU": "제주공항"

// key값을 통해 Data에 접근할 수 있다.
var airports: [String:String] = ["ICH": "인천공항", "CJU": "제주공항"] 
print("\(airports["ICH"])") 
print("\(airports["CJU"])")
```

### Dictionary 추가 기능
```swift
var dic: [String : String] = ["son" : "손오공", "bea" : "베지터", "pi" : "피콜로"]

//딕셔너리의 Element 갯수
dic.count

//빈 배열 확인
dic.isEmpty

// Element 추가
dic.updateValue("셀", forKey: "cel")

// Element 삭제
dic.removeValue(forKey: "bea")
```

```swift
func dicTest(){
    var dic: [String : Any] = ["name" : "joo", "age" : 20, "job" : "Developer", "isSingle" : true]
    
    //딕셔너리 추가
    dic.updateValue("address", forKey: "Seoul")
    
    //딕셔너리 수정
    dic.updateValue("name", forKey: "winman")
    
    //삭제
    dic.removeValue(forKey: "isSingle")
    
    //값 불러오기
    let introduce: String = "제 이름은" + (dic["name"] as! String) + "입니다. 사는 곳은 " + (dic["Seoul"] as! String)
    let doubleAge = (dic["age"] as! Int) * 2
    
    print(introduce)
    print(doubleAge)
    
    for (key, value) in dic{
        print(key, value)
    }
}
```

## 응용 실습 문제

#### 실습 1-1)기초
```swift
//시작과 끝수를 받아서 두 수 사이의 모든 수를 가지고 있는 배열 만들기
func insideNum(num1: Int, num2: Int) -> Array<Int>{
    var numArray = Array<Int>()
    
    for num in num1...num2{
        numArray.append(num)
    }
    
    return numArray
}

insideNum(num1: 1, num2: 4) // 1,2,3,4
```

#### 실습 1-2)기초
```swift
//정수 타입의 배열을 입력받아 모든 배열의 수의 합을 리턴하는 함수
func sumArray(arrayNum: Array<Int>) -> Int{
    var sumNum: Int = 0
    for num in arrayNum{
        sumNum += num
    }
    return sumNum
}

sumArray(arrayNum: insideNum(num1: 1, num2: 5)) // 15
```

#### 실습 1-3)기초
```swift
//딕셔너리에 있는 모든 데이터 출력하는 함수 >> 데이터: ["name":"joo", "age":20, "job":"Developer"]
let Data: [String : Any] = ["name" : "joo", "age" : 20, "job" : "Developer"]

func exportData(_ dicData:[String: Any]){
    for (key, value) in dicData{
        print("key : " + key + ", value : ", value)
    }
}

exportData(Data)
```

#### 실습 2-1)기초
```swift
//정수 타입의 배열을 받아서 배열안의 중복된 수를 모두 제거된 배열을 반환하는 함수
func removeDuplicate(of list: [Int]) -> [Int]{
    var resultList:[Int] = []
    
    for n in list{
        //.contains가 배열내에 n 값이 있는지 확인해준다.
        if !resultList.contains(n){
            resultList.append(n)
        }
    }
    return resultList
}
```
> .contains 함수로 새로 만든 배열에 중복된 숫자가 있는지 확인하여 없을때만 

#### 실습 2-2
```swift
//정수 배열을 입력받아, 배열의 요소 중 두 개를 선택하는 조합을 모두 포함하는 배열을 작성하세요.
//>> [1, 2, 3] -> [[1, 2], [1, 3], [2, 3]]

let exNum = [1,2,3,4,5]
func sperate(list: [Int]) -> [[Int]]{
    // 조합된 요소를 받아줄 배열 생성
    var resultList: [[Int]] = []
    for n in 0..<list.count{
        // 배열 첫수를 넣어준다.
        let firstV = list[n]
        //  n+1 식으로 마지막 배열은 for문을 안돌리게 된다.
        for i in n+1..<list.count{
            // 배열 두번째 수를 넣어준다.
            let secondV = list[i]
            resultList.append([firstV,secondV])
        }
    }
    return resultList
}
sperate(list: exNum)
```
> for문은 조건이 안맞을 경우 돌아가지 않는다.   

#### 실습 3-1)
```swift
//정수 타입의 배열을 입력받아서 오름차순으로 정렬된 배열을 만들어 리턴하시오.(정렬 함수 사용x)   (정렬의 효율은 보지 않습니다.)
let arrayNumEx3 = [4,5,1,2,7,2,7,2,3]

func sortArray(randomArr: [Int]) -> [Int]{
    
    var tempArr = randomArr
    var resultArr = [Int]()
    for _ in randomArr{
        var tempNum: Int = tempArr[0]
        var tempIndex: Int = 0
        if tempArr.count != 1{
            for num in 1...tempArr.count-1{
                if tempNum >= tempArr[num]{
                    tempNum = tempArr[num]
                    tempIndex = num
                }
                print(tempNum)
            }
            tempArr.remove(at: tempIndex)
            resultArr.append(tempNum)
            print(resultArr)
        }else{
            print(tempNum)
            resultArr.append(tempNum)
        }
        
    }
    
    return resultArr
}

sortArray(randomArr: arrayNumEx3)
```

#### 실습 3-2)
```swift
//>>에라토스테네스의 체 알고리즘을 이용하여  입력된 숫자까지의 모든 소수의 배열을 반환하는 함수
func eratosthenes(maxNum: Int) -> Array<Int>{
    // 입력된 숫자까지를 범위 연산자를 통해서 배열에 저장한다.
    var resultArray = Array(2...maxNum)
    // 마지막 배열임을 확인하는 Bool값
    var flag: Bool = true
    var tempIndex: Int = 0
    // 마지막 배열 전까지 while문을 반복한다.
    while flag {
        print(resultArray[tempIndex])
        var i: Int = 0
        for checkNum in resultArray{
            // 2부터 소수의 값으로 나눠 떨어지는 소수의 배수들을 차례대로 삭제하는 반복문
            if checkNum % resultArray[tempIndex] == 0 && checkNum / resultArray[tempIndex] != 1{
                resultArray.remove(at: i)
                i -= 1
            }
            i += 1
        }
        tempIndex += 1
        if tempIndex + 1 == resultArray.endIndex{
            flag = false
        }
    }
    
    return resultArray
}

eratosthenes(maxNum: 120)
```
> 에라스토테네스의 체는 2의 수부터 배수를 없에면 다음에 오게 되는 수가 소수가 되는 원리를 이용하여, 2부터 1씩 올려가며 배수를 삭제하는 알고리즘이다.
