# Swift 문법
> 2018.01.16 업데이트   

## 조건문
* 함수 내에서 실행되는 선택문   
* 특정 조건에 따라 선택적으로 코드를 실행시킨다.   
* 대표적인 조건문으로 if-else문과 swhich-case문이 있다.   
* 비교 연산자를 통해 나오는 Bool값이 나와야 된다.   
* 논리 연산자를 사용하여 조건 조합이 가능하다.   

## if-else문
* 조건이 참일 경우 if문의 대괄호 안의 코드가 실행된다.   
* 만약 조건이 거짓일 경우 else문 대괄호 안의 코드가 실행된다.   

```swift
if 조건 {
    // 조건이 만족되면 실행
}else{
    // 조건이 만족되지 않을 때 실핼
}
// * 조건 값은 참 or 거짓으로 표현되는 Bool을 사용한다.
```

### else if문
* if문 안에 else if를 추가하여 조건을 반복해서 추가할 수 있다.   

```swift
if 조건 {
    // 조건이 만족되면 실행
}else if{
    // 추가 조건문을 반복적으로 추가할 수 있다.
}else{
    // 조건이 만족되지 않을 때 실핼
}
// * 조건 값은 참 or 거짓으로 표현되는 Bool을 사용한다.
```
> swift에서는 0으로 나눗셈을 할 수 없기 때문에 두번째 값이 0일경우 바로 리턴하는 함수를 만든다.

## 연산자
### 산술 연산자
| 기호 |    예제    |  설명  |
|:----:|:----------:|:------:|
|   +  |  1 + 2 = 3 | 더하기 |
|   -  |  2 - 1 = 1 |  빼기  |
|   *  |  2 * 1 = 2 | 곱하기 |
|   /  | 10 / 3 = 3 | 나누기 |
|   %  | 10 % 3 = 1 | 나머지 |

### 비교 연산자
| 기호 |  예제  |          설명         |
|:----:|:------:|:---------------------:|
|  ==  | A == B | A와 B가 같다          |
|  >=  | A >= B | A가 B보다 크거나 같다 |
|  <=  | A <= B | A가 B보다 작거나 같다 |
|   >  |  A > B | A가 B보다 크다        |
|   <  |  A < B | A가 B보다 작다        |

### 논리 연산자
| 기호 |    예제   |                      설명                     |
|:----:|:---------:|:---------------------------------------------:|
|  ==  |   A && B  | A조건이 참이고, B조건이 참이면,참이다.             |
|  ㅣㅣ  |   A ㅣㅣ B  | A조건이나, B조건 둘중에 하나가 참이면,참이다.     |
|   !  | !(A ㅣㅣ B) | A ㅣㅣ B조건의 반대                             |

### 추가 연산자
* 복합연산자

| 기호 |  예제  |         설명        |
|:----:|:------:|:-------------------:|
|  +=  | a += 1 | a에 1의 값을 더하기 |
|  -=  | a -= 1 | a에 1의 값을 빼기   |

* 범위 연산자

|  기호 |  예제  |                 설명                |
|:-----:|:------:|:-----------------------------------:|
| a...b | 3...10 | a부터 b까지의 숫자 예) 3,4,5....10  |
| a..<b | 3..<10 | a부터 b앞까지의 숫자 예) 3,4,5....9 |

* identity 연산자   

| 기호 |       예제      |                      설명                      |
|:----:|:---------------:|:----------------------------------------------:|
|  === | name1 === name2 | name1과 name2는 같은 인스턴스를 참조하고 있다. |
|  !== | name1 !== name2 | name1과 name2는 다른 인스턴스를 참조하고 있다. |

### 삼항 연산자
* question이 참이면 answer1값을 거짓이면 answer2값은 지정한다.
* question과 answer1값 사이 ?의 앞 뒤에 스페이스를 주지 않으면 연산이 안되니 주의하자. 

```swift
let age =  20 var result: String = age > 19 ? "성년" : "미성년"

func trueNfalse(){
    return false
}
charm: String = trueNfalse() ? "true" : "false"
```

### if문 실습

#### 실습 1-1) 점수를 등급으로 반환해주는 함수
```swift
//1. 시험점수를 받아서 해당점수의 등급(Grade)을 반환해 주는 함수
//*Grade =  A+, A, B+, B, C+...
func gradeOfIf(score: Int) -> String{
    var grade: String = "F"
    if score <= 100{
        if 100 >= score && 95 <= score{
            grade = "A+"
        }else if 90 <= score{
            grade = "A"
        }else if 85 <= score{
            grade = "B+"
        }else if 80 <= score{
            grade = "B"
        }else if 75 <= score{
            grade = "C+"
        }
    }
    return grade
}

print(gradeOfIf(score: 89)) // B
```
> else if문으로 점수대 별로 조건을 줘서 

#### 실습 1-2) 등급을 받아서 학점으로 변환해주는 함수
```swift
//문제2. Grade받아서 Point로 변환해주는 함수 
//Point = 4.5, 4.0, 3.5, 3.0...
func pointOfIf(grade: String) -> Double{
    if grade == "A+"{
        return 4.5
    }else if grade == "A"{
        return 4.0
    }else if grade == "B+"{
        return 3.5
    }else if grade == "B"{
        return 3.0
    }else if grade == "C+"{
        return 2.5
    }else if grade == "C"{
        return 2.0
    }else{
        return 0
    }
}

print(pointOfIf(grade: gradeOfIf(score: 89)))
```
> else if 문으로 문자를 확인하여 점수를 변환해준다.

#### 실습 2-1) 짝수를 찾아 true를 반환해주는 함수
```swift
//<if>
//정수를 하나 입력받아 그 수가 짝수이면 true를  반환하는 함수
func findEvenNum(num: Int) -> Bool{
    let fEven: Int = num % 2
    if fEven == 0{
        return true
    }else{
        return false
    }
}

print(findEvenNum(num: 3)) //false
```
> 정수를 2로 나눈 나머지가 0일경우 짝수이기 때문에 0일 경우 true를 반환한다.

#### 실습 2-2) 입력받은 두 문자가 같을 때 true를 반환해주는 함수
```swift
//문자열 두개를 입력받아 두 문자열이 같으면 true를 반환해주는 함수
func equalString(firstStr: String, secondStr: String) -> Bool{
    if firstStr == secondStr{
        return true
    }else{
        return false
    }
}

print(equalString(firstStr: "a", secondStr: "b")) //false
```
> if문을 통해 문자열을 비교한 후 맞을 경우 true를 반환한다.

#### 실습 2-3) 두수를 입력받아 큰 수를 변환하는 함수
```swift
//두 수를 입력받아 큰 수를 반환하는 함수를 작성하세요.
func compNum(num1: Int, num2: Int) -> Int{
    if num1 > num2{
        return num1
    }else if num1 < num2{
        return num2
    }else{
        return 0
    }
}

print(compNum(num1: 2, num2: 1)) //2
```
> 두 수를 입력 받아 교차로 조건문을 만들어 큰 수를 반환한다.

#### 예제 2-4) 두 정수를 입력받아 두수의 나눗셈을 반환해주는 함수
```swift
// 두개의 정수를 입력받아 두수의 나누셈을 반환해주는 함수 (첫번째 값을 두번째 값으로 나눈다. 0으로 나누기를 할시 0을 반환)
func divNum(num1: Int, num2: Int) -> Int{
    if num2 == 0{
        return 0
    }
    let resultNum: Int = num1 / num2
    return resultNum
}

print(divNum(num1: 3, num2: 2)) //1
```

#### 실습 3-1) 정수 하나를 입력받아 3의 배수를 찾아주는 함수
```swift
//정수를 하나 입력받아 3의 배수이면 true를 반환해주는 함수
func findMultiple(num: Int) -> Bool{
    let fMult: Int = num % 3
    if fMult == 0{
        return true
    }
    return false
}

print(findMultiple(num: 3)) // true
```
> 입력 받은 수의 나머지가 0일 경우 3의 배수이기 때문에 true를 반환한다.

#### 실습 3-2) 윤년이 아닌지 판단해주는 함수
```swift
//윤년 구하기 문제(년도를 받아서 윤년인지 아닌지 판단하는 함수)
func confirmYear(year: Int) -> String{
    var flag: Bool = false
    
    if year % 4 == 0{
        flag = true
        if year % 100 == 0{
            if year % 400 == 0{
                flag = true
            }else{
                flag = false
            }
        }
    }
    if flag == false{
        return "\(year)은 윤달이 아닙니다."
    }else{
        return "\(year)은 윤달이 맞습니다.."
    }
}

print(confirmYear(year: 2)) // 2월은 윤달이 아닙니다.
```
> if문 안에 if문을 넣어 윤달에 대한 조건 함수를 만들었다.

#### 실습 3-3) 세수를 입력받아 양수를 확인해 주는 함수
```swift
//세 수를 입력받아 그 곱이 양수이면 true, 0 혹은 음수이면 false, 둘 다 아니면 에러를 발생시키는 함수를 작성하세요.
func threeNum(num1: Int, num2: Int, num3: Int) -> Bool{
    let resultNum: Int = num1 * num2 * num3
    var flag: Bool = true
    
    if resultNum <= 0{
        flag = false
    }
    return flag
}
 print(threeNum(num1: -1, num2: -2, num3: 0)) // false
```
> 세수의 곱을 상수에 넣어 그 상수가 0보다 작거나 같을 경우 false를 반환해준다.


## switch문
* 패턴 비교문
* 가장 첫번째 매칭되는 패턴의 구문이 실행된다.

### switch문 기본
* 각의 상태는 case 키워드를 통해 나타낼수 있다.    
* 각 case 상태 끝에는 콜론( : )을 작성해서 매칭 패턴을 종료한다.   
* 여러개의 case가 필요하면 콤마( , )를 통해 상태를 추가 할수 있다.  
* 각 case는 분기로 실행되며 매칭된 해당 case문이 종료되면 switch문을 종료시킨다.  
* 각 case의 상태는 switch 문의 value값에 매칭된 지점을 결정하며, 모든 value에 대해 매칭 되어야 한다. 만약 매칭되는 값이 없다면 default 키워드를 통해 기본 매칭값을 설정하며, default키워드는 마지막에 배치된다.  

```swift
switch some value to consider {
   case value 1:
   respond to value 1   
   case value 2,
        value 3:
        respond to value 2 or 3
    default:
        otherwise, do something else
}
```

### Interval Matching - switch
* switch문의 상태는 단순 value매칭을 넘어 좀 더 다양한 패턴을 통해 매칭이 가능하다.
* Interval Matching의 범위 연산자를 통해 해당 범위에 해당하는 value를 매칭할 수 있다.

```swift
//여러개의 grade를 입력받아서 grade의 평균을 반환해주는 함수
func gradeOfSwitch(score: Int) -> String{
    var grade: String = ""
    
    switch score {
    case 95...100:
        grade = "A+"
    case 90..<95:
        grade = "A"
    case 85..<90:
        grade = "B+"
    case 80..<85:
        grade = "B"
    case 75..<80:
        grade = "C+"
    default:
        grade = "F"
    }
    return grade
}
```

### 튜플 매칭
* 튜플을 사용해서 여러개의 value값을 동시에 확인할 수 있다.   
* 사용 가능한 모든 값에 대한 매칭은 와일드 카드 ( _ )를 통해서 매칭 가능하다.   
* 값 바인딩을 사용해서 case 내부에서 선언한 임시 값을 구문에서 사용이 가능하다.   
* where 문의 추가로 추가 조건을 넣을수 있다.   

#### 예제 1-1) switch 종합
```swift
func getPoint(somePoint:(Int,Int)) {
    switch somePoint {
    case (0, 0):
        print("\(somePoint) is at the origin")
    // 와일드 카드를 사용해서 모든 값에 대한 매칭이 가능하다.
    case (_, 0):
        print("\(somePoint) is on the x-axis")
    // 값 바인딩을 통해 case 내부에서 선언한 임시 값을 구문에서 사용할 수 있다.
    case (0, let y):
        print("on the y-axis with an y value of \(y)") 
    case (-2...2, -2...2): 
        print("\(somePoint) is inside the box")
    // where문으로 추가 조건을 넣을 수 있다.
    case let (x, y) where x == y:
        print("(\(x), \(y)) is on the line x == y") 
    default: 
        print("\(somePoint) is outside of the box")     
    } 
}
```

### switch문 문제

#### 실습 1-1) 여러개의 등급을 입력받아서 평균 학점을 반환해주는 함수
```swift
//여러개의 grade를 입력받아서 grade의 평균을 반환해주는 함수
func averageOfGrade(grades: String...) -> Double{
    var sumPoint: Double = 0
    for grade in grades{
        switch grade {
        case "A+":
            sumPoint += 4.5
        case "A":
            sumPoint += 4.0
        case "B+":
            sumPoint += 3.5
        case "B":
            sumPoint += 3.0
        case "C+":
            sumPoint += 2.5
        default:
            sumPoint += 2.0
        }
    }
    let avragePoint: Double = sumPoint / Double(grades.count)
    return avragePoint
}

print(averageOfGrade(grades: "A", "B", "A+")) // 3.83333333333333...
```
> 타입...을 사용하면 원하는 수만큼의 파라미터 값을 받을 수 있다. 여러개의 grade를 받아 for in loop를 통해 grade값을 switch 조건문으로 총합을 더해서 grades의 .count 갯수로 나눠  

#### 실습 2-1) 시험점수를 받아서 등급을 반환해주는 함수 - switch
```swift
//1. 시험점수를받아서해당점수의등급(Grade)을반환해주는함수
//*Grade =  A+, A, B+, B, C+...
func gradeOfSwitch(score: Int) -> String{
    var grade: String = ""
    
    switch score {
    case 95...100:
        grade = "A+"
    case 90..<95:
        grade = "A"
    case 85..<90:
        grade = "B+"
    case 80..<85:
        grade = "B"
    case 75..<80:
        grade = "C+"
    default:
        grade = "F"
    }
    return grade
}
```
> Interval Matching의 범위 연산자로 점수를 구분하여 점수를 반영하는 함수를 만들었다.

#### 실습 2-2) 등급을 받아서 점수로 반환해주는 함수
```swift
//문제2. Grade받아서 Point로변환해주는함수
//Point = 4.5, 4.0, 3.5, 3.0...
func pointOfSwitch(grade: String) -> Double{
    switch grade {
    case "A+":
        return 4.5
    case "A":
        return 4.0
    case "B+":
        return 3.5
    case "B":
        return 3.0
    case "C+":
        return 2.5
    default:
        return 0
    }
}
```
> switch로 문자를 구분하여 해당 점수를 반환하는 함수를 만들었다.

#### 실습 3-1) 튜플을 사용하여 도형 넓이 구해주는 함수
```swift
//문제 3. 튜플을 사용하여 도형 넓이 구하기
func areaOfShape(width: Double, length: Double, radian: Double) -> Double{
    // switch에 튜플을 사용하기 위해 상수에 입력된 값을 넣는다.
    let compareData = (width, length, radian)
    var area: Double = 0.0
    let pi = 3.14
    
    // 입력된 값에따라 도형을 구분하여 연산을 한다.
    switch compareData {
    case (let wid, let len, 0):
        area = wid * len
    case (0, 0, let radi):
        area = pi * radi * radi
    default:
        area = 0
    }
    return area
}

print(areaOfShape(width: 3, length: 2, radian: 0)) //6
```
> 튜플을 사용하여 입력된 값에따라 도형의 넓이를 구하는 함수

#### 실습 3-2) 튜플을 사용하여 도형 부피 구해주는 함수
```swift
//예제 1. 튜플을 사용하여 도형 부피 구하기
func volumeOf(height: Double, horizontal: Double = 0, vertical: Double = 0, radian: Double = 0) -> Double{
    var volume: Double = 0
    // switch에 튜플을 사용하기 위해 상수에 입력된 값을 넣는다.
    let tupleValue = (height, horizontal, vertical, radian)
    
    let pi: Double = 3.14
    
    switch tupleValue {
    case (let hei, let hor, 0, 0):
        volume = hei * hor * hor
    case (let hei, let hor, let ver, 0):
        volume = hei * hor * ver
    case (let hei, 0, 0, let radi):
        volume = pi * radi * radi * hei
    default:
        volume = 0
    }T
    return volume
}

volumeOf(height: 10, horizontal: 10) // 1000
```
> 튜플을 사용하여 입력된 값에따라 도형의 넓이를 구하는 함수

#### 실습 4-1) 정수를 입력받아 해당하는 월의 약어를 반환해주는 함수
```swift
//switch-case
//월을 입력받아 해당월의 이름을 반환해주는 함수 (ex: 1 >>> "Jan", 12 >>> "Dec", 13 >> "Error"
func switchMonth(month: Int) -> String{
    var mon: String = ""
    switch month {
    case 1:
        mon = "Jan"
    case 2:
        mon = "Feb"
    case 3:
        mon = "Mar"
    case 4:
        mon = "Apr"
    case 5:
        mon = "May"
    case 6:
        mon = "Jun"
    case 7:
        mon = "Jul"
    case 8:
        mon = "Aug"
    case 9:
        mon = "Sep"
    case 10:
        mon = "Oct"
    case 11:
        mon = "Nov"
    case 12:
        mon = "Dec"
    default:
        mon = "Error"
    }
    return mon
}
print(switchMonth(month: 3))
```
> 1부터 12까지 조건을 만들고 그 이외의 숫자가 들어갈 경우 "Error"를 반환한다.

#### 실습 4-2) 년/ 월을 입력받아 해당 달의 마지막 날을 반환해주는 함수
```swift
//년/월을 입력받아 해당 들의 마지막 날을 반환 해주는 함수(윤년 고려)
func interYear(year: Int) -> Bool{
    let interDay: Int = year % 4
    var flag: Bool = false
    
    switch interDay{
    // 4의 배수 중 400의 배수를 먼저 찾아주는 조건문
    case 0 where year % 400 == 0:
        flag = true
    // 4의 배수 중 윤달에 해당 되지 않는 100의 배수를 찾아주는 조건문
    case 0 where year % 100 == 0:
        flag = false
    case 0:
        flag = true
    default:
        flag = false
    }
    return flag
}

print(interYear(year: 2000))    
```
> 윤달을 확인하여 Bool값으로 반환해주는 함수

```swift
func finalDay(year: Int, month: Int) -> Int{
    var day: Int = 0
    
    switch month {
    case 1, 3, 5, 7, 8, 10, 12:
        day = 31
    // 윤달을 확인해주는 함수를 삼항 연산자에 담아 2월에 해당되는 case의 구문에서 실행
    case 2:
        day = interYear(year: year) ? 29 : 28
    default:
        day = 30
    }
    
    return day
}

print(finalDay(year: 2000, month: 2))
```
> 윤달이 포함된 2월을 제외한 나머지 달의 마지막 날 값을 구분해주고, 2월에는 함수를 삼항 연산자로 실행시켜 윤달을 확인하여 값을 리턴해준다.
