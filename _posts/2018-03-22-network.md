# Swift 문법
> 2018.03.22 업데이트   

## URI

### URI (Uniform Resource Identifier)
* URI is a string of characters used to identify a name or abstract / physical resource    
* 인터넷의 자원을 유일하게 식별하기 위한 통합 자원 식별자    
* 절대적 경로와 상대적 경로를 모두 포함하는 URL 과 URN 의 SuperSet   

### URL (Uniform Resource Locator)
* URL is a specific character string that constitutes a reference to a resource.   
* URL 은 어떤 자원의 위치에 대한 절대 경로값을 지닌 문자열    
* 어떤 특정 주소 또는 파일리소스에 접근하기 위한 주소값으로 흔히 HTTP 로 시작하는 웹주소로 인식하는 경우가 많지만, URL 의 한 형태에 해당하는 것으로 컴퓨터 네트워크상의 자원을 모두 나타낼 수 있음   

### URN (Uniform Resource Name)
* URN is persistent,location-independent identifiers for resources   
* 위치에 독립적이고, 지속되는 형태의 자원을 가르키기 위한 유일한 식별자   
* IETF 에서 표준 규격을 업데이트   

### URL vs URN
```
URL - 주소 / URN - 주민등록증

URL - 서울시 강남구 강남동 강남 아파트 1층 
URN - 철수(900101-1xxxxxx)         
    - 영희(900101-2xxxxxx)
```

### IRI (International Resource Identifier)
* Defined by the IETF in 2005 as a new internet standard to extend upon the existing URI   
* URI - ASCII character set    
* IRI - Fully supports international characters,  (mostly UTF-8)   
* 즉, IRI 는 URI 의 상위 개념으로서 확장된 버전    

## Byte Ordering
* 시스템이 내부적으로 데이터를 저장하고 표현하는 순서 CPU    
* 벤더에 따라 바이트 단위로 데이터를 받아 들이고 메모리에 저장하는 순서가 다른데서 기인
* Big Endian  /  Little Endian
* 그 외 Mixed, Middle, Bi 등의 Endian 이 있으나 많이 사용되지 않음   

### Big Endian
* Network Ordering 이라고도 함   
* 데이터를 상위 바이트부터 낮은 메모리 주소에 저장하는 형태   
```
e.g. 0x12345678   =>   0x12    0x34    0x56    0x78
                        낮은주소    -->     높은주소
```

### Little Endian
* Host Ordering 이라고도 하며, iPhone 도 여기에 해당    
* 데이터를 하위 바이트부터 낮은 메모리 주소에 저장하는 형태   
```
e.g. 0x12345678   =>   0x78    0x56    0x34    0x12
                        낮은주소    -->     높은주소
```

### Resolution
* Endian 통일 (Network Byte Order)    
    - 모든 시스템이 저장하는 방식을 통일시키기 어려운 상황이므로 모든 프로그램이 네트워크 전송 시, 약속된 공통의 Endian 을 사용하고 수신측에서 변환    
    - 네트워크 바이트 오더 표준 : Big Endian    
* Byte 단위 전송    
    -  Endian 문제는 Byte 단위로 저장할 때 순서의 차이에 의해 발생하므로, 애초에 1 Byte 단위로 데이터를 보내면 바이트 순서에 구애받지 않고 통신 가능    


```swift
import Foundation

class CardDataController {
    
    let cardList = [1,2,3,4,5,6,7,8,9,10,1,2,3,4,5,6,7,8,9,10]
    
    func shuffleCardList(){
        var tempList = cardList
        var resultList: [Int] = []
        
        while tempList.count != 0{
            let index: Int = Int(arc4random_uniform(UInt32(tempList.count)))
            resultList.append(tempList[index])
            tempList.remove(at: index)
        }
        print(resultList)
    }
    
}
```
