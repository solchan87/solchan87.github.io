# Swift 문법
> 2018.02.23 업데이트    

## Notification

### NotificationCenter
* 특정 이벤트가 발생 하였음을 알리기 위해 불특정 다수의 객체에게 알리기 위해 사용하는 클래스   
* 어떤 객체라도 특정 이벤트가 발생했다는 알림을 받을 것이라고 관찰자(Observer)로 등록을 해두면 노티피케이션 센터가 모든 관찰자 객체에게 알림을 준다

### Notification 주요 Method

```swift
// Initializing
open class var `default`: NotificationCenter { get }

// Add Observer
open func addObserver(_ observer: Any, selector aSelector: Selector, name aName: NSNotification.Name?, object anObject: Any?)
open func addObserver(forName name: NSNotification.Name?, object obj: Any?, queue: OperationQueue?, using block: @escaping (Notification) -> Swift.Void) -> NSObjectProtocol

// Post Notification
open func post(name aName: NSNotification.Name, object anObject: Any?,        userInfo aUserInfo: [AnyHashable : Any]? = nil)

// Remove Observer
open func removeObserver(_ observer: Any)
```

#### 예제
```swift
import UIKit

class ViewController: UIViewController {
    

    @IBOutlet weak var msgLb: UILabel!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        NotificationCenter.default.addObserver(forName: Notification.Name(rawValue: "notiKey"), object: nil, queue: nil) { (noti) in
            let msg = noti.object as! String
            var lbText: String = self.msgLb.text!
            lbText += msg
            
            self.msgLb.text = lbText
        }
    }
    
    // 클래스가 종료되는 시점에 옵저버를 삭제하는 메소드
    deinit {
        NotificationCenter.default.removeObserver(self)
    }

}
```

```swift
import UIKit

class NextViewController: UIViewController {

    @IBOutlet weak var msgTF: UITextField!
    
    override func viewDidLoad() {
        super.viewDidLoad()

        // Do any additional setup after loading the view.
    }

    @IBAction func msgBtn(_ sender: Any) {
        NotificationCenter.default.post(name: NSNotification.Name(rawValue: "notiKey"), object: msgTF.text)
        self.navigationController?.popViewController(animated: true)
        
    }
}
```