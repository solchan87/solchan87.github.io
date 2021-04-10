# Swift 문법
> 2018.03.02 업데이트

## Subscript
* 클래스, 구조체, 열거형의 collection, list, sequence의 멤버에 접근 가능한 단축문법인 Subscript를 정의 할수 있다. 
* Subscript는 별도의 setter/getter없이 index를 통해서 데이터를 설정하거나 값을 가져오는 기능을 할 수 있다. 
* `Array[index]` / `Dictionary[“Key”]` 등의 표현이 Subscript이다.

### Subscript 문법
```swift
//
subscript(index: Tyㅅe) -> Type { 
    get { 
        // return an appropriate subscript value here
    } set(newValue) {
        // perform a suitable setting action here
    } 
}

// get만 사용할 경우 get을 생략할 수 있다.
subscript(index: Type) -> Type {
    // return an appropriate subscript value here
}
```


## Extensions
* Extensions 기능은 기존 클래스, 구조, 열거 형 또는 프로토콜 유형에 새로운 기능을 추가합니다
* Extensions으로 할수 있는것은... 
    1. Add computed instance properties and computed type properties
    2. Define instance methods and type methods
    3. Provide new initializers
    4. Define subscripts
    5. Define and use new nested types 
    6. Make an existing type conform to a protocol

```swift
extension SomeType {
    // new functionality to add to SomeType goes here 
}extension SomeType: SomeProtocol, AnotherProtocol {
    // implementation of protocol requirements goes here
}
```