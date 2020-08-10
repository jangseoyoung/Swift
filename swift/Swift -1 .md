

## 기본 명명 규칙

> - 변수, 상수, 함수 , 메서드, 타입 등의 이름은 유니코드에서 지원하는 어떤 문자(한글, 한자, 영문, 숫자, 이모티콘 등등)라도 사용할 수 있다.
>
> **예외**
>
> - 스위프트에서 미리 정한 예약어 또는 키워드
> - 해당 코드 범위 내에서 미리 사용되는 기존 이름과 동일한 이름
> - 연산자로 사용될 수 있는 기호(+,-,*,/)
> - 숫자로 시작하는 이름
> - 공백이 포함된 이름
>
> - 함수, 메서드, 인스턴스 이름은 첫 글자를 소문자로 사용하는 소문자 카멜케이스(Lower Camel Case)를 사용
> - 클래스, 구조체, 익스텐션, 프로토콜, 열거형 이름은 타입의 이름이기 때문에 첫 글자를 대문자로 사용하는 대문자 카멜케이스(Upper Camel Case)를 사용
> - 대소문자를 구별함. Var != var

----

## 콘솔로그(Console Log)

> **print** : 단순 문자열 출력
>
> **dump** : 인스턴스의 자세한 설명까지 출력

----

## 문자열 보간법(String Interpolation)

- 변수 또는 상수 등의 값을 문자열 내에 나타내고 싶을 때 사용
- 문자열 내에 `\(변수나 상수)` 의 형태로 표기하면 이를 문자열로 치환해서 넣음.
- 프로그래머가 원하는 문자열로 치환 -> 변수나 상수 타입을 `CustomStringConvertible` 프로토콜을 준수하는 `description` 프로퍼티로 구현

----

## 선언

- **상수 선언**
  - let 이름 : 타입 = 값
  - let Name : Int = 50

- **변수 선언**
  - var 이름 : 타입 = 값
  - ex) var Name : Int = 50

> // 값의 타입이 명확하다면 타입은 생략 가능 
>
> // 나중에 할당하려고 하는 상수나 변수는 타입을 꼭 명시해주어야 함.
>
> // 변수는 차후에 다시 다른 값을 할당해도 문제가 없지만 상수는 에러남.
>
> // 변수 상수는 꼭 초기화를 해줄 것

----

## 데이터 타입

- 스위프트의 모든 데이터 타입 이름은 첫 글자가 대문자로 시작하는 **대문자 카멜케이스** 를 사용

> **Bool** : 0과 1은 int형으로 보기 때문에 불가능
>
> - 불리언 타입은 참(true) 또는 거짓(false)만 값으로 가진다.
>
> ```swift
> var isSameString : Bool = false
> isSameString = hello == "Hello"
> print(isSameString) // 출력 : true
> ```
>
> **Int** : 정수형
>
> **Unit** : 양수형 정수
>
> **Double** : 부동소수(64bit)
>
> **Float** : 부동소수(32bit) (Double에 비해 정확도가 떨어짐)
>
> **Chaacter** : 한글자 문자 (큰따옴표로 묶음, 유니코드로 표현가능한 모든 문자 표현 가능)
>
> **String** : 여러 문자를 넣어줄 수 있음. 연산자 이용하면 문자열을 합칠 수 있음. Character을 선언할 시 에러
>
> ```swift
> let hello : String = "Hello"
> let yagom : String = "yagom"
> var greeting : String = hello + " " + yagom + "!"
> print(greeting) // 출력 : hello yagom!
> ```
>
> **Any** : 모든 타입을 수용할 수 있음.
>
> **Anyobject** : Any보다는 조금 한정된 의미로 클래스의 인스턴스만 할당할 수 있음.
>
> **Nil** : Any에는 들어갈 수 없다. 아무것도 없음.

```swift
//메서드를 통한 대소문자 변환
var convertedStrig : String = ""
convertedString = hello.uppercased()
print(convertedString) // 출력 : HELLO
```

```swift
// 프로퍼티를 통한 빈 문자열 확인
var isEmptyString : Bool = false
isEmptyString = greeting.isEmpty
print(isEmptyString) // 출력 : false
```

----

## 특수문자

> \n : 줄바꿈 문자
>
> \\\ : 문자열 내에서 백슬래시를 표현하고자 할 때 사용
>
> \\" : 문자열 내에서 큰따옴표를 표현하고자 할 때 사용
>
> \t : 탭 문자, 키보드의 탭 키를 눌렀을 때와 같은 효과
>
> \0 : 문자열이 끝났음을 알리는 null문자

----

## 컬렉션 타입

>**Array** : 순서가 있는 리스트 컬렉션
>
>**Dictionary** : 키와 값의 쌍으로 이루어진 컬렉션
>
>**Set** : 순서가 없고, 멤버가 유일한 컬렉션

- 값을 없애고 싶을 때 Nil을 쓰면 됨.

----

## 함수

```swift
func 함수이름(매개변수1이름: 매개변수1타입, 매개변수2이름:매개변수2타입…)->반환타입{
함수 구현
return 반환값
}
```

```swift
func printYourName(name: String)->Void{
	print(name)
}
```

>// 반환값이 없는 경우 void생략 가능
>
>// 매개변수가 없으면 생략 가능하지만 괄호는 생략 불가능
>
>// 함수가 간단한 경우 줄바꿈을 하지 않아도 괜찮음.
>
>// 기본값을 갖는 매개변수는 매개변수 목록 중 뒤쪽에 위치하는 것이 좋음

- 전달인자 레이블
  - 함수를 호출할 때 매개변수의 역할을 좀 더 명확하게 하거나 함수 사용자의 입장에서 표현하고자 할 때 사용함.

```swift
func 함수이름(전달인자 레이블 매개변수1이름: 매개변수1타입, 전달인자 레이블…)->반환타입{
	함수 구현부
	return
}
```

>함수의 다양한 모양은 모두 섞어서 사용이 가능하다.
>
>- 스위프트는 함수형 프로그래밍 패러다임을 포함하는 다중 패러다임 언어이다.
>- 스위프트의 함수는 일급객체이므로 변수, 상수 등에 저장이 가능하다. 또한 매개변수를 통해 전달할 수 있다.
>- 반환타입을 생략할 수 있다.
>  - (매개변수 1타입, 매개변수 2타입...) -> 반환타입
>- 타입이 다른 함수는 할당할 수 없다.

----

## 조건문

- if문
  - if문은 무조건 bool

- switch문
  - switch문은 무조건 default가 있어야 하며 break는 안 써도 됨.
  - break를 없애고 싶으면 fallthrough
  - .. : 이상 ...: 이상 그리고 이하

----

## 반복문

- for - in
- while
- repeat - while

----

## 옵셔널(Optional)

- 옵셔널(Optional) : 값이 있을 수도, 없을 수도 있다.
  - 왜 필요한가 ? : nil의 가능성을 명시적으로 표현 -> 효율적, 예외상황 최소화로 안전

- Optional = enum + general

```swift
let optionalValue : Optional<Int> = nil
=  let optionalValue: Int? = nil
```

- Implicitly Unwarapped Optional : 암시적 추출 옵셔널(!)

```swift
var optionalValue : Int! = 100

switch optionalValue {
case .none:
	print(“This Optional variable is nil”)
case .some(let value):
	print(“Value is \(value)”)
}
```

> optionalValue = optionalValue + 1
>
> = optionalValue = nil
>
> = optionalValue = optionalValue +1//오류발생

- Optional : 박스

```swift
func printName(_ name: String){
	print(name)
}

var myName: String? = nil

printName(myName)
//전달되는 값의 타입이 다름으로 컴파일 오류발생
```

```swift
if-let
func printName(_ name: String){
	print(name)
}

var myName: String! = nil

if let name: String = myName{
	printName(name)
}else{
	print(“myName == nil”)
}
```

