## 프로퍼티

**종류**

>저장 프로퍼티(stored property)
>
>연산 프로퍼티(computed property)
>
>인스턴스 프로퍼티(instance property)
>
>타입 프로퍼티(type property)

**특징**

> 프로퍼티는 구조체, 클래스, 열거형 내부에 구현할 수 있다.
>
> `열거형 내부에는 연산 프로퍼티만 구현할 수 있다.`
>
> 연산 프로퍼티는 var로만 선언할 수 있다.

- 인스턴스 저장, 연산 프로퍼티

```swift
struct Student {
	//인스턴스 저장 프로퍼티
  var name : String = ""
  var `class`: String "Swift"
  var koreanAge : Int = 0
  
  //인스턴스 연산 프로퍼티 : 연산을 수행하기 위한 프로퍼티
  var westrnAge : Int {
		get {
      return koreaAge - 1
    }
    set (inputValue) {
      koreanAge = inputvalue + 1
      // westrnAge에 바로 저장되는 것이 아닌 koreanAge에서 연산을 해서 할당을 해 줌.
    }
  }
}
```

- 타입 저장 프로퍼티

```swift
static var typedescription : String = "학생"
//타입과 연관되어 저장되는 프로퍼티
```

- 읽기 전용 인스턴스 연산 프로퍼티

```swift
var selfIntroduction : String {
  get {
    return "저는 \(self.class)반 \(name)입니다"
  }
}
```

- 응용

```swift
struct Money {
  var currencyRate : Double = 1100
  var dollar : Double = 0
  var won : Double {
    get {
      return dollar * currencyRate
    }
    set {
      dollar = newValue / currencyRate // newValue : 환율
    }
  }
}
var moneyInMyPoket = Money()
moneyInMyPocket.won = 11000
print(moneyInMyPocket.won)
//11000
moneyInMyPocket.dollar = 10
print(moneyInMyPocket.won)
//11000
```

- 지역변수, 전역변수

> 저장 프로퍼티와 연산 프로퍼티의 기능은 함수, 메서드, 클로저, 타입 등의 외부에 위피한 지역/ 전역 변수에도 모두 사용 가능

```swift
var a: Int = 100
var b: Int = 200
var sum: Int {
  return a+b
}
print(sum) //300
```

----

## 프로퍼티 감시자

```swift
struct Money {
  //프로퍼티 감시자 사용
  var currencyRate : Double = 1100 {
    willSet(newRate) {
      print("환율이 \(currencyRate)에서 \(newRate)으로 변경될 예정입니다")
    }
    didSet(oldRate) {
      print("환율이 \(oldRate)에서 \(currencyRate)으로 변경되었습니다")
    }
  }
  //프로퍼티 감시자 사용
  var dollar : Double = 0 {
    //willSet의 암시적 매개변수 이름 newValue
    willSet {
      print("\(dollar)달러에서 \(newValue)달러로 변경될 예정입니다")
    }
    //didSet의 암시적 매개변수 이름 oldValue
    didSet {
      print("\(oldValue)달러에서 \(dollar)달러로 변경되었습니다")
    }
  }
  //연산 프로퍼티
  var won : Double {
    get {
      return dollar * currencyRate
    }
    set {
      dollar - newValue / currencyRate
    }
    // 프로퍼티 감시자와 연산 프로퍼티 기능을 동시에 사용할 수 없다.
  }
}
```

- 사용

```swift
var moneyInMyPocket : Money = Money()

//환율이 1100.0에서 1150.0으로 변경될 예정입니다
moneyInMyPocket.currencyRate = 1150
//환율이 1100.0에서 1150.0으로 변경되었습니다

//0.0달러에서 10.0달러로 변경될 예정입니다
moneyInMyPocket.dollar = 10
//0.0달러에서 10.0달러로 변경되었습니다

print(moneyInMyPocket.won)
//11500.0
```

> 프로퍼티 감시자의 기능은 함수, 메서드, 클로저, 타입 등의 외부에 위치한 지역/ 전역 변수에도 모두 사용 가능

- 프로퍼티 감시자와 전역변수/ 지역변수

```swift
var a : Int = 100{
  willSet {
    print("\(a)에서 \(newValue)로 변경될 예정입니다")
  }
  didSet {
    print("\(oldValue)에서 \(a)로 변경되었습니다")
  }
}
// 100에서 200으로 변경될 예정입니다
a = 200
// 100에서 200으로 변경되었습니다
```

----

## 상속

> 스위프트의 상속은 클래스와 프로토콜 등에서 가능하다.
>
> 열거형, 구조체는 상속이 불가능하다
>
> 스위프트는 다중상속을 지원하지 않는다.

```swift
import Swift
//class 이름 : 상속받을 클래스 이름 {
//	/*구현부*/
//}
class Person {
  func selfIntroduce() {
    print("저는 \(name)입니다")
  }
  //final 키워드를 사용하여 재정의를 방지할 수 있다.
  final func sayHello() {
    print("hello")
  }
  //타입 메서드
  //재정의 불가 타입 메서드 - static
  static func typeMethod() {
    print("type method - static")
  }
  //재정의 가능한 class 메서드라도 final키워드를 사용하면 재정의 할 수 없다.
	//메서드 앞의 `static`과 `final class`는 똑같은 역할을 한다.
  final class func finalClassMethod() {
    print("type method - final class")
  }
}
```

```swift
class Student : Person {
  //var name : String = "" <- 위에서 이미 상속을 받아왔기 때문
  var major : String = ""
  
  override func selfIntroduce() {
    print("저는 \(name)이고, 전공은 \(major)입니다")
  }
  override class func classMethod() {
    print("overriden type method - class")
  }
}
```

> static을 사용한 타입 메서드는 재정의 할 수 없다.
>
> override static func typeMethod() {	}

> final키워드를 사용한 메서드, 프로퍼티는 재정의 할 수 없다.
>
> override func sayHello() {	}
>
> override class func finalClassMethod ( ) {	}

```swift
let Seoyoung : Person = Person()
let Seungyun : Friend = Friend()

Seoyoung.name = "Seoyoung"
Friend.name = "Seungyun"
Friend.major = "Backend"

Seoyoung.selfIntroduce()
//저는 Seoyoung입니다

Seungyun.selfIntroduce()
//저는 Seungyun이고, 전공은 Backend입니다

Person.classMethod()
// type method - class

person.typeMethod()
// type method - static

Person.finalclassMethod()
// type method - final class

Student.classMethod()
// overriden type method - class
```

----

## 인스턴스의 생성과 소멸

- 이니셜라이저와 디이니셜라이저
- init, deinit

> 스위프트의 모든 인스턴스는 초기화와 동시에 모든 프로퍼티에 유효한 값이 할당되어 있어야 한다. 프로퍼티에 미리 기본값을 할당해 두면 인스턴스가 생성됨과 동시에 초기값을 지니게 된다.

```swift
class PersonA {
  //모든 저장 프로퍼티에 기본값 할당
  var name : String = "unknown"
  var age : Int = 0
  var nickName : String = "nick"
}
let jason : Person A = Person A()
jason.name = "jason"
jason.age = 30
jason.nickName = "j"
```

> 프로퍼티 기본값을 지정하기 어려운 경우에는 이니셜라이저를 통해 인스턴스가 가져야 할 초기값을 전달할 수 있음.

```swift
class PersonB {
  var name : String
  var age : Int
  var nickName : String
  
  //이니셜라이저
  init(name : String, age : Int, nickName : String) {
    self.name = name
    self.age = age
    self.nickName = nickName
  }
}
let hana : PersonB = PersonB(name: "hana", age: 20, nickName: "하나")
//let hana : PersonB = PersonB(name : "hana", age: 20, nickName : " ")
```

> 프로퍼티의 초기값이 꼭 필요 없을 때 : 옵셔널을 사용

```swift
class PersonC {
  var name : String
  var age : Int
  var nickName : String?
  
  init(name : String, age: Int, nickName : String) {
    self.name = name
    self.age = age
    self.nickName = nickName
  }
  init(name : String, age : Int){
    self.name = name
    self.age = age
  }
}
```

