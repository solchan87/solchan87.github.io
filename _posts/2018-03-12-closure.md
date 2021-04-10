# Swift 문법
> 2018.03.12 업데이트    

## Closure
* Closure란 코드의 블럭이자, 일급 객체로 완벽한 역할을 수행할 수 있다. 일급 객체란 전달인자로 보낼 수 있고, 변수/상수 등으로 저장하거나 전달할 수 있으며, 함수의 반환 값이 될 수 있다. 실제로 우리가 알고 있는 함수는 클로저의 한 형태로 이름이 있는 클로저이다.

### Closure 기본 문법
```swift
{ (parameters) -> return type in
    statements
}
```
> 클로저의 내용(statements)은 `in` 키워드로 시작하며 이 키워드는 클로저 인자와 반환 타입의 정의가 끝났고 클로저 내용이 시작함을 가르킴.

### Closure의 형태
* 전역 함수는 이름은 있지만 아무런 값을 가지지 않는 클로저.   
* 중첩 함수는 이름이 있고, 내부 함수에서 값을 획득할 수 있는 클로저.   
* 클로저 표현식은 둘러싸고 있는 컨텍스트에서 값을 획득하는 가벼운 문법으로 작성된 이름 없는 클로저.   

* Swift 클로저 표현식은 일반적인 경우에 깨끗하고, 명확한 스타일로 최적화되어 간략하고, 깔끔한 문법을 가짐. 이러한 최적화는 다음을 포함함.   
    - 컨텍스트로부터 인자와 반환 값 타입을 유추
    - 단일 표현식 클로저로부터 명확한 반환
    - 축약 인자 이름
    - 후행 클로저 문법 (Trailing Closure)

### Basic Closure
```swift
let simpleClosure = {
  print("This is SimpleClosure!!")  //This is SimpleClosure!!
}
simpleClosure()

let closureParameter = { (str: String) -> Int in
  return str.count
}
let count = closureParameter("Swift")
print(count)  //5
```

### Inline closure
```swift
func printSwift() {
  print("Swift")
}
let arg = {
  print("Inline Closure!!")
}
func closureParamFunction(closure: () -> Void) {
  closure()
}
closureParamFunction(closure: printSwift)
closureParamFunction(closure: arg)
closureParamFunction(closure: {
  print("explicit closure parameter name")
})
```

### Trailing Closure
* 긴 클로저 표현식을 함수의 마지막 인자로 함수를 전달할 필요가 있다면 후행 클로저로 유용하게 대신 사용할 수 있음. 후행 클로저는 함수 표현식으로 함수 괄호 밖에서 작성되어 지원함.
```swift
func closureParamFunction2(closure1: () -> Void, closure2: () -> Void) {
  closure1()
  closure2()
}

closureParamFunction2(closure1: {
  print("inline")
}, closure2: {
  print("inline")
})

closureParamFunction2(closure1: {
  print("inline")
}) {
  print("trailing")
}
```

### Syntax Optimization
```swift
func performClosure(param: (String) -> Int) {
  print(param("Swift"))
}

performClosure(param: { (str: String) -> Int in
  return str.count
})
```
> `param`은 `Int`를 반환하기 때문에 타입을 유추할 수 있어 `-> Int`가 생략이 가능하다.

```swift
performClosure(param: { (str: String) in
  return str.count
})

performClosure(param: { str in
  return str.count
})

performClosure(param: {
  return $0.count
})
```
> 단일 표현식 클로저는 클로저 정의에서 return 키워드를 생략한 단일 표현식 결과를 암시적으로 반환할 수 있음.

```swift
performClosure(param: {
  $0.count
})

performClosure(param: ) {
  $0.count
}

performClosure() {
  $0.count
}

performClosure { $0.count }
```

