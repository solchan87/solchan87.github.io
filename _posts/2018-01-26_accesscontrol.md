# Swift 문법
> 2018.01.26 업데이트    

## 접근 제어
* 외무 모듈에서의 접근을 제어하는 수단    
* 캡슐화, 은닉화를 위해 사용      
* 모드 & 소스파일    
    * 모듈 : 배포할 코드의 묶음 단위, 통상 프레임워크나 라이브러리, 어플리케이션이 모듈의 단위가 될수 있다.   
    * 소스파일 : 하나의 스위프트 소스코드 파일(FileName.swift)   

### open
* open 클래스는 정의된 모듈 내에서와 정의된 모듈을 가져오는(imports) 모든 모듈에서 서브클래스화(subclassed) 할 수 있다.   
* open 클래스 멤버는 정의된 모듈내에서와 정의된 모듈을 가져오는(imports) 모든 모듈에서 서브클래스(subclasses)에 의한 오버라이드(overridden)가 할 수 있다.   

### public
* public접근이나 더 제한적인 접근 레벨의 클래스는 정의된 모듈내에서만 서브클래스화(subclassed) 할 수 있습니다.   
* public접근이나 더 제한적인 접근 레벨의 클래스 멤버는 정의된 모듈내에서만 서브클래스(subclasses)에 의한 오버라이드(overridden) 할 수 있습니다.   

### internal(기본값)
* 요소들은 정의된 모듈의 모든 소스파일에서 사용 할수 있지만, 모듈 밖의 모든 소스 파일에서는 사용 할수 없다. 
* 앱 또는 프레임 워크의 내부 구조로 정의 할때, 일반적으로 internal 접근을 사용한다.

### fileprivate
* 자신이 정의된 소스파일에서만 요소(entity)를 사용할수 있도록 제한 한다.
* file-private 접근은 상세 정보가 전체 파일내에서 사용될때 일부 특정 함수의 세부 구현을 숨길때 사용한다.

### private
* 선언된 영역(enclosing)에서만 요소를 사용할 수 있도록 제한합니다. 
* private접근은 하나의 선언 안에서 상세 정보를 사용할때 일부 특정 함수의 세부 구현을 숨길때 사용합니다.


```swift
public class SomePublicClass{
    public var somePublicProperty = 0
    var someInternalProperty = 0
    fileprivate func someFilePrivateMethod(){}
    privatefunc somePrivateMethod(){}
} 
class SomeInternalClass{
    var someInternalProperty = 0
    fileprivate func someFilePrivateMethod(){}
    private func somePrivateMethod(){}
}
fileprivate class SomeFilePrivateClass{
    func someFilePrivateMethod(){}
    privatefunc somePrivateMethod(){}
} 
private class SomePrivateClass{
    func somePrivateMethod(){}
}
```

## Property

### 저장 프로퍼티 (Stored Properties)
* 가장 일반적인 프로퍼티   
* 값을 저장하는 용도로 사용된다.   
* 클래스, 구조체에서만 인스턴스와 연관된 값을 저장한다.   
* 초기값을 설정 할 수 있습니다.  

```swift
struct Subject{
    var name: String
    var score: Int
}
class Person{
    var name: String
    var gender: String
    var blood: String?
}
```

#### 지연 저장 프로퍼티 (Lazy Stored Properties)
> 시동 시 인스턴스 초기화가 많을경우 로딩이 길어지는 단점이 있기 때문에, 시점을 다르게 하여 최초 실행 시 초기화를 진행한다.

* 지연 저장된 속성은 처음 프로퍼티가 사용되기 전 까지 초기값이 계산되지 않은 특성을 가지고 있는 프로퍼티이다.  
* 지연 저장 속성은 lazy keyword를 선언 앞에 작성한다.  
* let은 지연 저장 프로퍼티로 설정할 수 없다.  
* 초기화하는데 오래걸리거나, 복잡한 초기화 과정이 있는 변수의 경우 지연저장을 사용하면 좋다 .

```swift
class ViewController: UIViewController{
    //init 시점이 아닌 사용이 되는 시점에 초기화한다. 
    lazy var cal:Calculator = Calculator()
    override func viewDidLoad(){
        super.viewDidLoad()cal.average(student: Student())
    }
}
```

#### Property Observers
> 특정한 값의 변화에 따라서 데이터 변환하거나, 연산이 실행될때 사용할 수 있다.   

* 프로퍼티 값의 변화를 감시하고 그에 따라 대응한다.    
* 초기값이 설정된 저장 프로퍼티에서 사용 가능하다.   
* 프로퍼티의 값이 설정될때마다 호출된다.   
* didSet(값이 들어간 후), willSet(값이 들어가기 직전) 키워드를 통해 값 변화의 직전 직후를 감지 할수 있다.   
* 값이름 미지정시 oldValue(변하기 전 값), newValue(변한 후 값)가 기본값으로 지정된다.   

```swift
// 프로퍼티 옵저버 예제
var changeValue: Int = 0{
    didSet(oldV){ // 값이 변한 후 실행
        print("oldValue is \(oldV)") // 기본값은 oldValue
    }willSet(willV){ // 값이 변하기 직전 실행
        print("newValue is \(willV)") // 기본값은 newValue
    }
}
changeValue = 4
//newValue is 4
//oldValue is 0
```

### 연산 프로퍼티 (Computed Properties)
> 실질적인 값을 저잘할 수 없으며, 함수와 비슷한 개념이다. 하는 일은 프로퍼티에 값을 넣고 뺄때(get & set) 연산 프로퍼티를 사용한다.   

```swift
// 연산 프로퍼티의 기본적인 문법
var name: String{
    get{
        return
    }
    set(inputName){
        // set에 잇풋 프로퍼티 네임이 없을 경우 newValue(기본값)로 대처할 수 있다.
    }
}
```

```swift
// 데이터를 한번 더 확인한 후 연산작업을 할 경우에 아래 구문으로 사용할 수 있다.
private var _name: String?

var name: String?{
    get{
        return _name
    }
    set{
        // newValue(기본값 사용)
    }
}
```

#### read-only 연산 프로퍼티
* 읽기 전용 연산프로퍼티 작성시 get 키워드 없이 바로 작성할수 있다.     
* 쓰기 전용 연산 프로퍼티는 작성할수 없다.   

```swift
struct Cuboid{
    var width = 0.0, height = 0.0, depth = 0.0
    var volume: Double {
        returnwidth * height * depth
    }
}
```

### 타입 프로퍼티 (TypeProperties)
> 타입 프로퍼티는 인스턴스 전체가 아닌 하나의 타입(속성)을 정의할 수 으며, .문법으로 정의할 속성을 정한다.

* 인스턴스의 속성이 아닌, 타입에 따른 속성을 정의 할수 있다.  
* static 키워드를 사용해서 타입 프로퍼티를 설정할수 있으며, 클래스의 경우 연산 프로퍼티의 오버라이드를 지원하기 위해서는 class 키워드를 사용해서 클래스 타입에서 연산 프로퍼티를 설정해야 한다.(class키워드는 저장 프로퍼티는 사용불가) 
* 값을 가져올때는 클래스의 이름을 통해서 가져올 수 있다.

```swift
struct AudioChannel {
    static let level = 10
    static var maxLevel = 0
    var currentLevel: Int = 0 {
        didSet {
            if currentLevel > AudioChannel.level {
                currentLevel = AudioChannel.level            
            }
            if currentLevel > AudioChannel.maxLevel {
                AudioChannel.maxLevel = currentLevel
            }
        }
    }
}
```

#### Method
* 메서드는 특정 타입에 관련된 함수를 뜻한다.  
* 함수의 문법과 같다.  
* 인스턴스의 기능을 수행하는 인스턴스 메서드와 타입자체의 기능을 수행하는 타입 메서드로 나눌수 있습니다.

#### self Property
* 모든 인스턴스는 self 프로퍼티를 가지고 있다.  
* self 프로퍼티는 자기 자신을 가르키고 있는 프로퍼티이다.   
* Type Method안에서의 self는 클래스 자체를 가르키고, instance Method안에서는 self는 인스턴스를 가리킨다.

```swift
struct Point {
    var x = 0.0, y = 0.0
    func isToTheRightOf(x: Double) -> Bool {
        // self. 문법으로 구조체의 x 를 가리킨다.
        return self.x > x
    }
}
```

#### Value Type 프로퍼티 수정
* 기본적으로 구조체와 열거형의 값타입 프로퍼티는 인스턴스 메소드 내에서 수정이 불가능 하다.  
* 그러나 특정 메소드에서 수정을 해야 할경우에는 `mutating` 키워드를 통해 변경 가능하다.

```swift
struct Point { 
    var x = 0.0, y = 0.0
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
}
```

## 참고문서
* [[접근제어 - 때로는 까칠하게..tistory]](http://kka7.tistory.com/29)