# Swift 문법
> 2018.01.15 업데이트

## 변수
1. **변수명**  
   * 명명 규칙에 따라서 작성   
   * 유니코드 문자를 포함하여 모든 문자가 포함될 수 있다.(한글 가능)   
   * 변수안에 들어있는 데이터를 표현해 주는 이름으로 작성   
   * 중복 작성 불가 (한 클래스, 함수, 구문 안에서)   

2. **명명 규칙**
   * 시스템 예약어는 사용할 수 없다     
   * 변수명 시작에 숫자가 올 순 없지만 변수명에는 포함될 수 있다     
   * 공백을 포함할 수 없다   
   * 변수명은 lowerCamelCase로 작성   
   * 클래스 명은 UpperCamelCase로 작성  

### 변수 타입  
1. **Int**
   - 정수형 타입 Integer  
   - Int : +/- 부호를 포함한 정수, Uint -부호를 포함하지 않는 0을 포함한 양의 정수  
   - 최대 값과 최소 값은 .max와 .min 프로퍼티를 통해 알 수 있다.  
   - Int8, Int16, Int32, Int64, UInt8, UInt16, UInt32, UInt64의 타입으로 나눠져   있는데 기본은 시스템 아키텍쳐에 따라서 달라진다.   
   - 접두어에 따라 진수를 표현할수 있다. (2진법 0b, 8진법0o, 16진법0x)  

2. **Double**  
   - 부동 소수점을 사용하는 실수형 타입  
   - 64비트의 부동소수점은 Double, 32비트 부동 소수점은 Float으로 표현한다.  
   - Double은 15자리,Float은 6자리의 숫자를 표현가능   

3. **String**
   - 문자의 나열, 문자열이라고 한다.  
   - Character와 마찬가지로 유니코드로 이뤄져 있다.  
   - 문자열을 다루기 위한 다양한 기능이 제공된다.(hasPrefix, uppercased, isEmpty등)  
   - 문자열을 Character로 분해하여 꺼낼 수 있다.  
   - String의 문자 하나를 부를때는 Character를 사용한다.  

4. **Bool** 
   - 참(true)과 거짓(false)를 나타내는 타입   

5. **튜플**
   - 정해지지 않은 데이터 타입의 묶음  
   - 소괄호 ( ) 안에 타입을 묶음으로 새로운 튜플타입을 만들수 있다. `(Int, Int)`, `(String, Int, String)`   
   - 각 타입마다 이름을 지정해 줄수도 있다. `(name:String, age:Int)`   
```swift
    var sampleTuple: (Int, sName: String, Int) = (3, "joo", 4)
    print(sampleTuple.0) // 3
    print(sampleTuple.sName) // joo
```

6. **캐스팅 변환**
   - 데이터 유형이 같지 않을 경우 데이터간 연사이 안되기 때문에 캐스팅 후 연산을 할 수 있다.
```swift
     var stringNum: String
     var doubleNum: Double

     let intNum: Int = 3

     stringNum = String(intNum) //int to String
     doubleNum = Double(intNum) //int to Double
```

## 함수 
> Swift 프로그램에서 연산을 담당하는 부분 

1) Argument Name and Parameter Names   
   - 인수명은 함수 호출시 사용 되는 이름 (Argument-아규먼트) 
   - 매개변수는 함수 내부에서 사용 되는 변수명.(Parameter-파라메터)  
   - 인수명은 생략가능하며, 생략하면 매개변수명이 인수명로 사용된다   
   - 인수명을 제거하고 싶으면 와일드카드 ( _ )를 사용한다   

```swift
//함수 예시
func fName(argumentName paramName: Int) -> Int{
    return 1
}
```

* inout 파라미터
   - 매개변수는 상수값이다.  
   - 만약 매개변수의 값을 변경해야 한다면 inout 키워드를 사용하여inout매개변수로 지정 해야 한다.  
   - inout매개변수 지정은 타입 앞에 inout keyword를 작성해준다.  
   - inout 변수가 지정된 함수의 인수앞에서 &가 붙어야 한다.(단! 변수를 사용해서 대입할 수 있다. 직접 값 대입 불가)  

```swift
// inout 예시
var num1 = 10
var num2 = 8
print(num1,num2) //10 8
func swapTowInts(_ a: inout Int, _ b: inout Int){
    let tempA = a
    a = b
    b = tempA
}
    
swapTowInts(&num1, &num2)
print(num1,num2) //8 10
```

### 함수 실습
#### 실습 1) 도형 계산식 실습
```swift
// 도형 계산식 실습

// 정사각형 둘레 및 넓이 구하기
class Calcsquare{
    func squareArea(length: Int) -> Int{
        return length * length
    }
    func squarePerimeter(length: Int) -> Int{
        return length * 4
    }
}

// 직사각형 둘레 및 넓이 구하기
class CalcRectangle{
    func rectangleArea(width: Int, length: Int) -> Int{
        return width * length
    }
    
    func rectanglePerimeter(width: Int, length: Int) -> Int{
        return (width * 2) + (length * 2)
    }
}

// 원 둘레 및 넓이 구하기
class CalcCircle{
    let pi: Double = 3.14
    
    func circleArea(radius: Double) -> Double{
        return pi * radius * radius
    }
    func circleCircumference(radius: Double) -> Double{
        return 2 * pi * radius
    }
}

// 삼각형 넓이 구하기
class CalcTriangle{
    func triangleArea(height: Double, base: Double) -> Double{
        return (height * base) / 2
    }
}

// 사다리꼴 넓이 구하기
class CalcTapezoid{
    func tapezoidArea(height: Double, widthA: Double, widthB: Double) -> Double{
        return (widthA + widthB) * height / 2
    }
}

// 정육면체 부피 구하기
class CalcCube{
    func cubeVolume(side: Int) -> Int{
        return side * side * side
    }
}

// 직육면체 부피 구하기
class CalcRectangular{
    let pi: Double = 3.14
    
    func rectangularSoildVolume(width: Int, length: Int, height: Int) -> Int{
        return width * length * height
    }
}


// 원기둥 부피 구하기
class CalcCircular{
    let pi: Double = 3.14
    
    func circularCylinderVolume(radius: Double, height: Double) -> Double{
        return pi * radius * radius * height
    }
}
// 원구 부피 구하기
class CalcSphere{
    let pi: Double = 3.14
    
    func sphereVolume(radius: Double) -> Double{
        return pi * radius * radius * radius * (4/3)
    }
}
// 원뿔 부피 구하기
class CalcCone{
    let pi: Double = 3.14
    
    func coneVolume(radius: Double, height: Double) -> Double{
        return pi * radius * radius * height * (1/3)
    }
}
```

> 간단하게 식을 함수에 대입해서 할 수 있다.

#### 실습 2) 도형 계산식 실습
```swift
// 인치를 센치로 바꾸는 함수
func inchToCm(_ inch: Double) -> Double{
    let toCm: Double = 2.54
    return inch * toCm
}
// 센치를 인치로 바꾸는 함수
func cmToInch(_ cm: Double) -> Double{
    let toInch: Double =  0.39370
    return cm * toInch
}
// 제곱미터를 평 단위로 바꾸는 함수
func squareMToPyeong(_ squareM: Double) -> Double{
    let toPyeong: Double = 0.3025
    return squareM * toPyeong
}
// 평 단위를 제곱미터로 바꾸는 함수
func pyeongToSquareM(_ pyeong: Double) -> Double{
    let toSquare: Double = 3.30579
    return pyeong * toSquare
}
// 섭씨를 화씨로 바꾸는 함수
func tempCToTempF(_ tempC: Double) -> Double{
    let toTempF: Double = 1.8
    let zeroF: Double = 32
    
    return tempC * toTempF + zeroF
}
// 화씨를 섭씨로 바꾸는 함수
func tempFToTempC(_ tempF: Double) -> Double{
    let toTempC: Double = 1.8
    let zeroC: Double = 32
    
    return (tempF - zeroC) / toTempC
}
// kb를 mb로 바꾸는 함수
func kbToMb(_ kb: Double) -> Double{
    let toMb: Double = 0.001
    
    return kb * toMb
}
// mb를 gb로 바꾸는 함수
func mbToGb(_ mb: Double) -> Double{
    let toGb: Double = 0.001
    return mb * toGb
}
```

> 변환 공식을 함수에 대입해서 풀 수 있다.

#### 실습 2-1) 시간을 hhmmss로 받아 초 단위로 반환하는 함수 - String
```swift
// 시간을 hhmmss로 받아 초 단위로 바꾸는 함수 - String
func timeToSecond(hhmmss time:String) -> Int{

    // 인덱스 번호를 받아 substring으로 문자열을 잘라주는 함수
    func stringTotime(startNum: Int, endNum: Int) -> Int{
        let startIndex = time.index(time.startIndex, offsetBy: startNum) //시작 인덱스
        let endIndex = time.index(time.endIndex, offsetBy: endNum) // 끝 인덱스
        let subTiem: Substring = time[startIndex ..< endIndex] // 시작 인덱스 부터 끝 인덱스 앞 까지
        let resultTime: Int! = Int(String(subTiem)) // 받은 substring을 String > Int로 바꿔주는 함수
        
        return resultTime
    }
    //인덱스 번호를 넣어 원하는 자리의 문자열 추출
    let hour: Int = stringTotime(startNum: 0, endNum: -4)
    let min: Int = stringTotime(startNum: 2, endNum: -2)
    let second: Int = stringTotime(startNum: 4, endNum: 0)
    
    //초 단위로 바꾸는 과정
    return (hour * 3600) + (min * 60) + second
}
print(timeToSecond(hhmmss: "112233"))
```

> hhmmss(시간)을 스트링으로 받았을 경우 처리할 수 있게 받을 스트링을 인덱스번호를 바탕으로 잘라서 인트로 변환하여 초 단위를 구할 수 있게 했다. 하지만, 들어오는 값에 대한 예외처리는 하지 못했다.

#### 실습 2-2) 시간을 hhmmss로 받아 초 단위로 반환하는 함수 - Int
```swift
// 시간을 hhmmss로 받아 초 단위로 바꾸는 함수 - Int
func changeToSecond(from time: Int) -> Int{

    // 입력된 시간이 변화가 가능하도록 변수로 설정
    var remainTime: Int = time
    // 나머지를 구하는 방법으로 뒤에 두자리수 초 단위를 구함
    let second: Int = remainTime % 100
    // 뒤에 두자리 수를 없에기 위해서 100으로 나눠주는 함수
    remainTime = remainTime / 100
    // 나머지를 구하는 방법으로 뒤에 두자리수 분 단위를 구함
    let min: Int = remainTime % 100
    // 마지막 두자리 수를 구해 시간 단위를 구함
    remainTime = remainTime / 100
    let hour: Int = remainTime % 100
    
    //초 단위로 바꿔주는 함수
    return (hour * 3600) + (min * 60) + second
}
```

> hhmmss(시간)을 Int(정수)로 받았을 경우 나눗샘과 나머지를 구하는 방식으로 정수를 잘라서 초단위를 구할 수 있었다.

#### 실습 3-1) 함수 기초 문제
```swift
//<기초>
//1-a 이름(문자열)을 받아서 이름을 출력하는 함수
func printName(name: String){
    print(name)
}
//1-b 나이*(정수)를 받아서 나이를 출력하는 함수
func printAge(age: Int){
    print(age)
}
//1-c.이름과 주소를 입력받아 자기소개글을 프린트 하는 함수(자기소개글은 자유)
func print(name: String, address: String){
    print("나는 \(name)입니다. 지금은 \(address)에 살고 있습니다.")
}
//정수를 하나 입력받아서 2로 나눈 값을 반환해주는 함수
func halfInt(num: Int) -> Int{
    return num / 2
}
//정수를 하나 입력받아서 제곱을 반환해주는 함수
func squareInt(num: Int) -> Int{
    return num * num
}
```

#### 실습 3-2) 함수 응용 문제
```swift
//<응용 - 다중 입력, 반환>
//2-a. 두개의 정수를 입력받아 두수의 합을 반환해주는 함수
func sumInt(num1: Int, num2: Int) -> Int{
    return num1 + num2
}
//2-b. 두개의 정수를 입력받아 두수의 차를 반환해주는 함수
func subInt(num1: Int, num2: Int) -> Int{
    return num1 - num2
}
//2-c. 두개의 정수를 입력받아 두수의 곱을 반환해주는 함수
func mulInt(num1: Int, num2: Int) -> Int{
    return num1 * num2
}
//2-d. 두개의 정수를 입력받아 두수의 나누셈을 반환해주는 함수
func divInt(num1: Int, num2: Int) -> Int{
    return num1 / num2
}
//<응용>
//부모님과 내 나이를 입력 후 그 나이차를 프린드 하는 함수 (ex: "어머니의 나이는 40세이고 내 나이는 20살이므로 우리의 나이차이는 20살 입니다.)
func parentsAge(pAge: Int, mAge: Int){
    let subAge: Int = pAge - mAge
    print("어머니의 나이는 \(pAge)이고 내 나이는 \(mAge)이므로 우리의 나이 차이는 \(subAge)입니다.")
}

//시험점수 여러개를 입력받아서(4개이상) 평균을 반환해주는 함수
func scoreByAverage(scoreA: Double, scoreB: Double, scoreC: Double, scoreD: Double) -> Double{
    let average: Double = (scoreA + scoreB + scoreC + scoreD) / 4
    return average
}
```

#### 실습 3-3) 캐스팅 문제
```swift
//<캐스팅>
//정수를 하나 입력받아서 실수로 변환 후 반환해주는 함수
func intToDouble(num: Int) -> Double{
    let castingNum: Double! = Double(num)
    return castingNum
}

//정수를 두개를 입력받아 두수를 합친수를 출력하는 함수 (ex: 3,4 입력시 >>> 34 /// 1,0 입력시 >>> 10)
func sumIntToString(num1: Int, num2: Int) -> String{
    let sumInt: String = String(num1) + String(num2)
    return sumInt
}
```

#### 실습 3-4) 캐스팅 문제 반올림 - rounded
```swift
//실수를 하나 입력받아서 소수점 첫번재 자리에서 반올림 후 정수를 반환해주는 함수
func roundOfDouble1(num: Double) -> Int{
    // 실수의 소수점을 반올림 해서 정수로 바꿔주는 함수
    let result: Int! = Int(num.rounded())
    return result
}
```

> rounded를 사용하여 반올림을 할 수 있다.

#### 실습 3-5) 캐스팅 문제 반올림 - reminder
```swift
//실수를 하나 입력받아서 소수점 첫번재 자리에서 반올림 후 정수를 반환해주는 함수
func roundOfDouble2(num: Double) -> Int{
    
    // 나머지를 구하는 연산자 %에서 double로 나눠지지 않는 것을 수동으로 대체한 파라미터
    let modul: Double = num.remainder(dividingBy: 1.0)
    print(modul)

    // 나머지 값의 크기를 바탕으로 반올림 여부를 정하는 함수
    if modul >= 0{
        return Int(num)
    }else{
        return (Int(num) + 1)
    }
}
```

> %는 정수로만 연산이 되도록 되있는데 remainder를 통해 예외적으로 실수로 계산할 수 있다.

#### 실습 3-6) 캐스팅 문제 반올림
```swift
func roundOfDouble3(num: Double) -> Int{
    
    let tempA: Double = num * 10
    let tempB: Int! = Int(tempA) % 10
    
    let tempC: Int = Int(num)
    if tempB >= 5{
        return tempC + 1
    }else{
        return tempC
    }
}

print(roundOfDouble3(num: 1.63244))
```

> 나눗셈과 곱샘으로 소숫점 자리를 정수의 위치로 올린다음 정수 첫째자리를 구하여, 조건문으로 반올림을 구분하는 함수이다.