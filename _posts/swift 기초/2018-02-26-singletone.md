# Swift 문법
> 2018.02.26 업데이트    

## Singletone Pattern
* 싱글톤 이란 : 어플리케이션 전 영역의 걸쳐 하나의 클래스의 단 하나의 인스턴스만(객체)을 생성하는 것을 싱글톤 패턴이라고 한다.  
* 사용이유 : 어플리케이션 내부에서 유일하게 하나d만 필요한 객체에서 사용(셋팅, 데이터 등)   
* 클래스 메소드로 객체를 만들며 static을 이용해서 단 1개의 인스턴스만 만든다.   
* 앱 내에서 공유하는 객체를 만들 수 있다.

### Singletone Pattern
```swift
class SingletonClass { 
    // MARK: Shared Instance 
    static var sharedInstance: SingletonClass = SingletonClass()
    // Can't init is singleton - 외부에서 초기화를 할 수 없다.
    private init() {
        //초기화가필요하면 private로생성
    }
}
```
> UserDefault, NotificationCenter, UIScreen, UIApplication 등이 싱글톤이다.   



