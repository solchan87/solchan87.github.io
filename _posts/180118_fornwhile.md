# Swift 문법
> 2018.01.18 업데이트    

## 반복문
* 반복적으로 실행되는 코드를 만드는 구문   
* 대표적인 반복문으로 while문과 for문이 있다.   

## While문
* 조건이 참일 경우 구문 반복 실행   

```swift
while 조건{
    // 구문 실행
}
```

#### 예제 1) 구구단
```swift
func timeTable(_ times: Int){
    print("\(times)단")
    // while문에과 구구단 피연산자로 사용될 count
    var count: Int = 1
    // 9단 까지만 구하기 때문에 10 이전에 멈추는 while문을 사용한다.
    while count < 10 {
        print("\(times) * \(count) = \(times * count)")
        // 카운트 값을 늘려줘야 반복문이 끝날 수 있다.
        count += 1
    }
}
```

### while문 실습

#### 실습 1-1) 삼각수 구하기
```swift
// 삼각수 구하기 : 삼각수란 1부터 모든 수의 합이다. ex)삼각수 10 = 55
// * 메소드 실행 : triangular(num: 10) // triangular(num:-1)

func triangular(_ num: Int) -> Int{
    // parameter 값을 변수로 사용하기 위해 또 다른 변수에 대입한다.
    var triNum: Int = num
    // 중간 결과 값을 저장하기 위한 함수
    var sumNum: Int = 0
    while triNum > 0 {
        sumNum += triNum
        triNum -= 1
    }
    return sumNum
}

print(triangular(10))
```
> parameter값은 기본적으로 상수로 선언되기 때문에 변수로 사용하기 위해서 변수에 대입한 다음 연산을 진행했다.

#### 실습 1-2) 각 자리수를 더하는 메소드
```swift
// 각 자리수를 더하는 메소드
func addAll(_ num: Int) -> Int{
    // parameter값을 변수로 저장하기 위한 구문
    var addNum: Int = num
    var resultNum: Int = 0
    while addNum > 0{
        // 10으로 나눈 나머지 값으로 1의 자리는 구한다
        resultNum += addNum % 10
        // 10으로 나눈 값으로 1의자리 수를 제거한다.
        addNum = addNum / 10
    }
    return resultNum
}

print(addAll(6))
```
> 10으로 나눈 나머지 값은 1의 자리 숫자를 구할 수 있고 10으로 나눈 값은 1의자리를 제거한 나머지 값만 가져올 수 있다.

```swift
// 숫자 리버스 함수
func revers(_ num: Int) -> Int{
    var revNum: Int = num
    var resultNum: Int = 0
    while revNum > 0{
        //resultNum의 함수에 10을 곱해서 자리수를 올려준다.
        resultNum = resultNum * 10
        resultNum += revNum % 10
        revNum = revNum / 10
    }
    return resultNum
}

print(revers(573831))

```
> 실습 1-2 함수에 `resultNum = resultNum * 10`만 추가하게 되면 임시 저장 함수에 있는 수를 10단위 올려줘서 반전이 가능하다.

## for-in 문
* 배열의 항목, 숫자의 범위 또는 문자열의 문자(Character) 시퀀스를 반복하려면 for-in 반복문을 사용한다.

```swift
let numbers = [1,2,3,4,5]
for number innumbers{ 
    print("\(number)")
}
```

### 숫자 범위의 연산
> 범위 연산자 `..<`, `...`를 통해 반복의 범위를 정할 수 있다.

```swift
for index in 1...5{
     print("\(index) times 5 is \(index * 5)") 
}
```

### 와일드 카드
> 문자상에는 필요하지만 실제 동작에서는 사용하지 않는 변수 이름에 `_`를 대신 사용하여 표현한다.

```swift
let base = 3
let power = 10
var answer = 1
for_in 1...power {
    answer *= base
}
```

#### 예제 1) 구구단 함수를 for문으로 표현
```swift
// for문을 이용한 구구단 함수
func timesTableFor(times: Int){
    // for문을 1부터 9까지 9번을 반복해주는 구문
    for count in 1...9{
        print("\(times) * \(count) = \(times * count)")
    }
}
```

### for-in문 실습

#### 실습 1-1) 팩토리얼 함수 만들기
```swift
// 팩토리얼 - 정수 하나를 받아서 그 수 의 팩토리얼을 구하시오
// 정수를 1부터 해서 해당 정수까지의 숫자를 모두 곱하는 함수
func factorial(num: Int) -> Int{
    // 1부터 시작하기 때문에 1을 곱해주는 함수 2...num으로 반복 조건을 줘도 됨
    var resultNum: Int = 1
    for countNum in 1...num{
        // *= 으로 resultNum = resultNum + countNum 을 대신할 수 있다.
        resultNum *= countNum
    }
    return resultNum
}

factorial(num: 5) // 120
```
> `+=`, `-=`, `*=`, `/=`로 a = a + 1같은 식을 a += 1로 간단하게 정리할 수 있다.

### 응용 실습 문제

#### 실습 1-1) collatz 함수 만들기 - while
```swift
// 정수가 짝수 일때는 2로 나누고 홀수 일때는 3을 곱한 수 1을 빼면 마지막으로 오는 수가 1이 되는 함수
func collatzWhile(num: Int) -> Int{
    var calcNum: Int = num
    var count: Int = 0
    // 정수 계산 값이 최종값인 1이 맞는지와 count값이 500을 넘는지를 확인하는 구문
    while calcNum != 1 && count < 500{
        // 정수를 2로 나눈 나머지 값이 0일경우 짝수이다.
        if calcNum % 2 == 0{
            calcNum /= 2
        }else{
            calcNum *= 3
            calcNum += 1
        }
        // while문이 1번 돌아갈때마다 체크하기 위하여 count에 1씩 더해주는 구문
        count += 1
    }
    // 최종적으로 나온 count의 값이 500일 경우 -1로 반환해주는 삼항 연산자 구문
    return count == 500 ? -1 : count
}

print(collatzWhile(num: 6))
```
> while문으로 변수의 조건에 맞춰서 count값을 반환하는 함수이다. 계산값이 1이 아니고 count 값이 500이 넘지 않도록 하는 조건문을 돌려 해당하는 조건에 대해 연산을 하는 if문을 넣어 만들었다.

#### 실습 1-2) collatz 함수 만들기 - for
```swift
func collatzFor(num: Int) -> Int{
    var count: Int = 0
    var calcNum: Int = num
    
    for _ in 1...500 {
        if calcNum % 2 == 0{
            calcNum /= 2
        }else{
            calcNum *= 3
            calcNum += 1
        }
        count += 1
        if calcNum == 1{
            break
        }else if count == 500{
            count = -1
            break
        }
    }
    
    return count
}

//print(collatzFor(num: 999999999999999993))
```
> while문과는 반대로 1부터 500까지만 for문을 돌려주는 함수를 만들고 만족하는 계산값(1)이 나왔을 떄 break로 조건문을 나와 결과값 count를 리턴해주는 함수이다.

#### 실습 2)
```swift
// 연습문제 - 알고리즘(Harshad 수)
// 양의 정수 x 가 하샤드 수이려면 x의 자릿수의 합으로 x가 나누어져야 합니다.
func harshadWhile(num: Int) -> Bool{
    var n: Int = num
    var divNum: Int = 0
    while n != 0 {
        divNum += n % 10
        // while문이 돌아갈 때마다 10의자리씩 줄여주는 구문
        n /= 10
    }
    // 마지막까지 나온 결과값을 바탕으로 삼항연산자를 만들었다.
    return (num % divNum) == 0 ? true : false
}

harshadWhile(num: 18)
```
> 10으로 나눠준 몫은 1의자리를 생략해주는 식이기 때문에 이렇게 계속 하게 되면 결국 0이 되기 마지막 자리가 변수의 최고자리 숫자이다.