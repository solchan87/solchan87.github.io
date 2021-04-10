# Swift 문법
> 2018.02.06 업데이트    

## Delegate Pattern

### 프로토콜(Protocol)
* 프로토콜은 원하는 작업이나 기능을 구현되도록 메서드, 프로퍼티등으로 요구사항의 청사진을 정의합니다.  
* 클래스, 구조체, 열거형은 프로토콜을 채택하면, 프로토콜에서 요구한사항에 대해 구현해야 됩니다.   
* 프로토콜을 통해 공통적인 작업을 강제할 수 있으며, 해당 프로토콜을 채택한 사람이 구현한 메소드에 대한 정보도 알수 있다

#### Protocol 문법
```swift
protocol Runable { 
    var regCount: Int { get set }
    func run()
}

class Animal: Runable {
    var regCount: Int = 0
    func run() {

    }
}
```

#### Protocol 채택
* 프로토콜 간 채택한 모든 것들을 클래스에서 선언해줘야 된다.

```swift
protocol Runable { 
    var regCount: Int { get set }
    func run()
}

protocol Flying: Runable {
    var wingCount: Int { get set }
}

class Animal: Runable {
    var regCount: Int = 0
    var wingCount: Int = 0
    func run() {

    }
}
```

#### 추상 클래스로의 Protocol
* 프로토콜을 추상 클래스처럼 사용할 수 있다.
* 다음과 같은 클래스가 있고, racing이라는 함수를 구현하려고 한다면
```swift
class Dog: Runable {
    //... 
}
class Horse: Runable {
    //... 
}
func racing(animals: [Runable]) -> Runable {

}

// 프로토콜 타입으로 사용 가능하다.
let winner: Runable = racing(animals: [Dog(), Horse()])
```

### Delegate
* 델리게이트는 클래스나 구조체에서의 일부분의 할일을 다른 인스턴스에게 대신하게 하는 디자인패턴!
* 뷰가 받은 이벤트나 상태를 ViewController에게 전달해 주기위해 주로 사용된다. (ex : `UIScrollViewDelegate`)
* ViewController를 통해 View구성에 필요한 데이터를 받는 용도로도 사용(ex : `UITableViewDataSource`)

#### CustomDelegate 만들기
* Delegate 선언부
```swift
class CustomView: UIView {
    var delegate: CustomViewDelegate?
    override func layoutSubviews() {
        delegate?.viewFrameChanged(newFrame:self.frame)
    } 
}
protocol CustomViewDelegate {
    func viewFrameChanged(newFrame:CGRect)
}
```

* Delegate 구현부
```swift
class ViewController: UIViewController, CustomViewDelegate {
    override func viewDidLoad() {
        super.viewDidLoad()
        let custom = CustomView()
        custom.delegate = self
    }
    func viewFrameChanged(newFrame: CGRect) { 
        // 뷰의 프레임이 변경될 때마다 불림 
    }
}
```