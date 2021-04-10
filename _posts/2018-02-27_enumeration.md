# Swift 문법
> 2018.02.27 업데이트    

## Enumeration (열거형)
* 그룹에 대한 연관된 값을 정의하고 사용가능한 타입.    
* 다른 언어와 달리 항목 그자체가 고유의 값으로 해당 항목에 값을 매칭 시킬 필요가 없다.(C계열 언어는 Int타입의  값이 매칭됨.   
* 원시값(rawValue)이라는 형태로 실제 값(정수, 실수, 문자등)을 부여 할수 있다.   
* 열거형의 이니셜라이즈를 정의 할수 있으며, 프로토콜 준수, 연산프로퍼티, 메소드등을 만들수 있습니다.

### Enumeration 문법
```swift
enum enumName {
    case enumItem1
    case enumItem2
    case enumItem3
}
```

#### 예제1)
```swift
// CompassPoint 자체가 타입
enum CompassPoint {
    case north
    case south
    case east
    case west
}

var directionToHead = CompassPoint.west
directionToHead = .north
```
> 열거형의 대표적인 예로 Optional이 있다.  

#### 예제2)
```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}

// 연관 열거형 값 지정
var productBarcode = Barcode.upc(8, 85909, 51226, 3)
productBarcode = .qrCode("ABCDEFGHIJKLMNOP")

// 연관 열거형 값 불러오기
switch productBarcode {
    case .upc(let numberSystem, let manufacturer, let product, let check) :
        print("UPC: \(numberSystem), \(manufacturer), \(product), \(check).”) 
    case .qrCode(let productCode) :
        print("QR code: \(productCode)")
}

// Pattern Matching 값이 매칭할 경우 정상 바코드 구문 실행   
let productBarcode = Barcode.upc(8, 85909, 51226, 3)

if case let Barcode.upc(8, companyCode, productCode, 3) = productBarcode {
    // 정상바코드
    print(companyCode) 
    print(productCode) 
}
```
> 항목에 값을 지정해서 사용하며, 스위치문을 통해서 값을 가지고 와 사용할 수 있다.

### Row Value
```swift
enum ASCIIControlCharacter: Character {
    case tab = "\t"
    case lineFeed = "\n"
    case carriageReturn = "\r"
}
// 첫번째 값에 rowValue를 지정해주면, 지정한 수부터 하나씩 번호가 지정된다
enum Planet: Int{ 
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
}
let earthsOrder = Planet.earth.rawValue
    // earthsOrder is 3 
// Initializing from a Raw Value
let possiblePlanet:Planet? = Planet(rawValue: 1)
    // possiblePlanet is mercury

// rowValue를 지정하지 않을경우 자동으로 값이 들어간다.
enum CompassPoint: String { 
    case north, south, east, west 
}
let sunsetDirection = CompassPoint.west.rawValue
    // sunsetDirection is "west"
```
> .rawValue 프로퍼티를 통해 원시값을 가져올수 있다.

#### Initializing from a Raw Value
* 원시값 열거형에서는 초기화 함수를 통해 instance를 만들수 있다. (rawValue:값 지정으로 인해 생성) 
* 초기화를 통해 만든 인스턴스는 옵션널 변수로 만들어 진다.

## 에러처리

### 예외처리
* 프로그램의 오류 조건에 응답하고 오류 조건에서 복구하는 프로세스입니다 
* Swift는 런타임시 복구 가능한 오류를 던지고, 포착하고, 전파하고, 조작하는 기능을 제공합니다.  
* 에러는 Error 프로토콜을 준수하는 유형의 값으로 나타냅니다. 실제로 Error프로토콜은 비어 있으나 오류를 처리할수 있는 타입임을 나타냅니다.

#### 열거형의 에러 표현
* 열거형은 에러를 표현하는데 적합합니다.
```swift
enum VendingMachineError: Error {
    case invalidSelection
    case insufficientFunds(coinsNeeded: Int) 
    case outOfStock 
}
```

### 에러 발생
* throw키워드를 통해 에러를 발생 시킵니다.
```swift
throw VendingMachineError.insufficientFunds(coinsNeeded: 5)
```

### 에러 전달
* 함수의 작성중 에러가 발생할수 있는 함수에는 매개변수 뒤에 throws 키워드를 작성하여 에러가 전달될수 있는 함수를 선언합니다.
```swift
//에러전달 가능성 함수
func canThrowErrors() throws -> String
//에러전달가능성이없는함수
func cannotThrowErrors() -> String
```

### 에러 처리
* 함수가 에러를 throw하면 프로그램의 흐름이 변경되므로 에러가 발생할 수있는 코드의 위치를 신속하게 식별 할 수 있어야합니다.  
* 이 장소를 식별하기 위해 `try` 나 `try?`, `try!`를 사용할수 있습니다.  
* 발결된 에러를 처리하기 위해 do-catch 문을 사용해서 에러를 처리 합니다.  

#### do - catch
```swift
do {
    try expression
    statements   
} catch pattern 1 {
    statements
} catch pattern 2 where condition {
    statements
}
```
> throws를 통해서 전달해주는 에러만 잡을 수 있다.

