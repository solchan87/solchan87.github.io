# Swift 문법
> 2018.01.31 업데이트    

## 옵셔널 (Optional)
> Swift가 가진 가장 큰 특징 중 하나가 Optional이다. 이는 값이 있을 수도 없을 수도 있음을 나타낸다.

#### nil
```swift
class Person{
    var name: String
    init(name: String) {
        self.name = name
    }
}

let person2: Person
print(person2.name)
```
> 변수 선언 후 초기화 하지 않은 상태를 nil이라 한다.

### Type Safety
> Swift에서는 nil상태에서 속성을 참조하거나 함수 실행시 발생하는 에러를 막기위해서 옵셔널(optional)을 사용한다. 옵셔널을 사용할때는 불안정성을 가진 변수에 `?`를 선언하여 가능성을 염두할 수 있도록 한다.

* nil인 상태에서 속성을 참조하거나, 함수를 실행시 발생하는 error로 인한 코드의 불안정성 내포.  
* Swift의 중요한 특징 중 하나는 Safety이다. 
* Type Safety를 위해 컴파일러 수준의 nil 체크한다.
* 만약 nil인 변수 선언을 해야할 경우 optional을 사용한다.    
* optional은 두가지 가능성을 가질수 있는데한개는 값이 있음을 나타내고 또 다른 한가지는 nil일 가능성을 내포하고 있다.(?기호 사용)

```swift
var person: Person!
var name: String!
var age: Int!
var subjects: [Int]!
```
> 해당 변수에는 값이 항상 존재한다.

```swift
var person: Person?
var name: String?
var age: Int?
var subjects: [Int]?
```
> 해당변수가값이있을수도있고, nil일수도있다!

### Unwrapping
* UnwrappingOptional 변수에 값이 있음을 확인하여 일반변수로 전환해준다.

#### 강제 해제(Forced Unwrapping)
```swift
func testFuc(optionalStr:String?) {
    if optionalStr != nil {
        let unwrapStr:String = optionalStr!
        print(unwrapStr)
    }
}
```

#### 선택적 해제(Optional Binding)
```swift
func testFuc(optionalStr:String?) {
    if let unwrapStr:String = optionalStr {
        print(unwrapStr) 
    }
}
```

* Optional Binding 변수가 두개 이상일 경우 `,`콤마를 통해 옵셔널 바인딩을 추가하고, 또 조건도 추가 할수 있다.
```swift
func isNumber(inputNum1:String, inputNum2:String) -> Bool{
    if let firstNumber = Int(inputNum1), let secondNumber = Int(inputNum1){
        return true
    }else{
        return false
    }
}
```

### Early Exit - guard문
```swift
guard 조건값 else{
    //조건값이거짓일때실행
    //종료조건이항상필요
}
```

