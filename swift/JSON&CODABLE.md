## JSON

### JavaScript Object Notation

- 네트워크를 통해 데이터를 주고받는 데 자주 사용되는 경량의 데이터 형식

```swift
{"users": [
  {
    "firstName" :"Ray",
    "lastName" : "Villalobos",
    "joined" : {
      "month" : "January",
      "day" : 12,
      "year" : 2012
    }
  },
  {
    "firstName" : "John",
    "lastName" : "Jones",
    "joined" : {
      "month" : "April",
      "day" : 28,
      "year" : 2010
    }
  }
]}
```

- JSON에서 대괄호의 의미는 "배열"을 의미한다.
- 객체는 반드시 name-value의 쌍, 쌍들은 무조건 쉼표로 구분되어야 함
- object {key:value}

> JSON
>
> - simplest data interchange format
> - lightweight text-based structure
> - easy to read
> - key-value pairs
> - used for serialization(직렬화) and transmission of data between the network the network connection
> - `independent programming language and platform`

**HTTP** : HyperText Transfer Protocol

-  server -> request -> client
- server <- response <- client

**AJAX** : Asynchronous JavaScript And XML

- XHR : XMLHttpRequest
- fetch() API

**XML** : markup언어 (html같은)

----

## Codable

### A type that can convert itself into and out of an external representation

#### : 자신을 변환하거나 외부표현(external representation)으로 변환할 수 있는 타입

```swift
typealias Codable = Decodable & Encodable
```

```swift
protocol Encodable
	A type that can encode itself to an external representation
protocol Decodable
	A type that can decode itself from an external representation
```

***Codable은 Decodable과 Encodable 프로토콜을 준수하는 타입(프로토콜)이다.***

> Decodable : 자신을 외부표현 (external representation)에서 디코딩 할 수 있는 타입
>
> Encodable : 자신을 외부표현 (external representation)에서 인코딩 할 수 있는 타입

// 외부표현 : JSON

- Codable은 Class, Struct, Enum에서 모두 사용할 수 있음.
- Codable을 채택했다는 의미 = Class, Struct, Enum을 serialize / deserialize할 수 있다는 것을 의미

```swift
struct Person : Codable {
  var name : String
  var age : Int
}

let encoder = JSONEncoder()
let zero = Person(name: "Zedd", age: 100)
let jsonData = try? encoder.encode(zedd)
```







// 출처 : https://zeddios.tistory.com/373