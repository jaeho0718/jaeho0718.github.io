---
title: Swift Data
author: Lee Programmer
date: 2023-07-02
category: Jekyll
layout: post
---

2023 WWDC에서 **Swift Data**라는 흥미로운 프레임워크가 발표되었다. Swift Data에 대해 알아보자

> [Preserving your app’s model data across launches](https://developer.apple.com/documentation/swiftdata/preservingyourappsmodeldataacrosslaunches#Configure-the-model-storage)

모델 선언
-------------

Swift Data에서 저장하기 위한 모델을 만들떄 **Model** 매크로를 이용하면된다.


```swift
    import SwiftData

    @Model
    class Trip {
        var name: String
        var destination: String
        var startDate: Date
    }
```

`@Model` 매크로는 해당 객체가 `PersistentModel` 프로토콜에 따르도록 업데이트한다. 또한 해당 객체의 변화를 트래킹할 수 있도록 `Observable`프로토콜에 따른다.

기본적으로 *noncomputed properties*를 모두 저장한다. 기본 타입 (Bool, Int, String...)뿐 아니라 `Codable`에 따르는 모든 타입도 저장할 수 있다.

모델 속성의 행동 커스텀하기
-------------

`Attribute`는 SwiftData가 관리하는 모델 객체의 속성이다. 기본적으로 default behavior는 `ufficient`이다.

모델 객체 속성의 *behavior*를 정하기 위해서는 **Attribute** 어노테이션을 사용하면 된다.

```swift 
    @Attribute(.unigue) var name: String
```

모델 속성에 다른 모델 혹은 모델 컬렉션이 있으면, Swift Data는 해당 모델과 다른 모델 사이의 *relation*을 관리한다. 기본적으로 연관된 다른모델 삭제시, **Relation attributes**는 *nil*로 정해진다. 다른 **Deletion rule**을 적용하고 싶으면 **Relationship** 어노테이션을 이용하면 된다.

```swift
    @Relationship(.cascade) var accomodation: Accomodation?
```

> DeleteRule에 대한 것은 문서로 대체하겠다. [RelationShipDeleteRule](https://developer.apple.com/documentation/swiftdata/relationshipdeleterule)

위에서 SwiftData는 *noncomputed attributes*를 모두 저장한다고 했다. 만약 저장하지 않길 원한다면 어떻게 해야할까?

`Transient` 매크로를 이용하면된다.

```swift
    @Transient var destinationWeather = Weather.current()
```

모델 저장소 설정하기
-------------

SwiftData가 모델을 저장하고 요구되는 스키마를 생성하기 전에 어떤 모델을 저장하고, 사용되는 저장소에 대해 설정해야한다. 아래 modifier를 통해 설정할 수 있다.

```swift
    modelContainer(for: ,inMemory: ,isAutosaveEnabled: ,isUndoEnabled: ,onSetup: )
```

SwiftUI를 사용하지 않으면 model container를 만들면 된다.

```swift
    import SwiftData

    let container = try ModelContainer([Trip.self, Accommodation.self])
```

> 만약 모델이 `Relationship`을 포함하고, *Destination 모델 타입*을 리스트에 포함하지 않더라도 SwiftData는 자동적으로 *Destination Model` 타입을 포함한다.

모델 저장하기
-------------

런타임에서 모델 객체의 인스턴스들을 관리할 때 `model context`를 이용하면된다.

Main actor에 바인딩된`model container`를 가져오기 위해서는 `modelContext`를 사용하면된다.

```swift
    import SwiftUI
    import SwiftData

    struct ContentView: View {
        @Environment(\.modelContext) private var context
    }
```

SwiftUI를 사용하지 않거나 View밖에서는, `container`의 `context`를 사용하면 된다.

```swift
    let context = container.mainContext
```

위 두개의 인스턴스에서 반환된 context는 주기적으로 저장되지않은 변화점들을 확인하고, 자동으로 저장한다. 

만약 context를 만든다면, `autosaveEnabled`를 `true`로 설정하면된다.

SwiftData가 모델을 저장하고 변화를 트래킹하기 위해서는 모델의 인스턴스를 `context`에 `insert`해주면 된다.

```swift
    var trip = Trip(name: name, 
                    destination: destination,
                    startDate: startDate,
                    endDate: endDate)

    context.insert(trip)
```

`insert`후 context의 `save()` 메소드를 통해 즉작적으로 저장할 수 있다.

`context`는 자동적으로 모델 인스턴스들의 변화와 이후 저장들을 추적한다.

`insert`외 `delete`, `fetch`, `enumerate`에 관한 것은 [여기서 확인하면](https://developer.apple.com/documentation/swiftdata/modelcontext) 된다.

모델 불러오기
-------------

SwiftData에서는 [`Query`](https://developer.apple.com/documentation/swiftdata/query) property wrapper과 [`Fetch Descriptor`](https://developer.apple.com/documentation/swiftdata/fetchdescriptor)를 제공한다.

`@Model` 매크로는 Model 객체를 `Observable`에 따르도록 만들기 때문에, 불러온 모델 인스턴스들에 변화가 생기면 SwiftUI를 refresh한다.

```swift
    import SwiftUI
    import SwiftData

    struct ContentView: View {
        @Query(sort: \.startDate, order: .reverse) var allTrips: [Trip]

        var body: some View {
            ForEach(allTrips) {
                TripView(for: $0)
            }
        }
    }
```

View 밖에서 모델을 불러오기 위해서, `context`의 fetch methods를 이용하면 된다.

`FetchDescriptor`는 `Predicate`, `batching`, `offset`, `prefetching`를 설정할 수 있다.

Predicate
-------------

> A predicate is a logical condition that evaluates to a Boolean value

```swift
    let messagePredicate = #Predicate<Message> { message in
        message.length < 100 && message.sender == "Jermy"
    }
```

`Predicate` 매크로는 **컴파일 시** 클로져를 `predicate`를 전환한다.

`Predicate`에서 다음 연산을 사용할 수 있다.

1. 사칙연산 (+,-.*,/,%)
2. 단항 빼기 (-)
3. 범위 (..., ..<)
4. 비교 (<, <=, >=, ==, !=)
5. 삼항 조건 (? :)
6. 부울
7. 옵셔널 (?, ??, !)
6. 타입 (as?, as!, is)
8. 시퀀스 연산 (`allSatisfy()`, `filter()`, `contains()`, `contains(wher: )`, `starts(with: )`)
9. Subscript 와 멤버 접근 ([], .)

`Predicate`는 중첩 선언, `for`과 같은 flow control,변수 수정을 포함할 수 없다. 하지만 해당 범위에서 변수를 참조할 수 있다. 중첩 조건도 가능하다.

```swift
    let messagePredicate = #Predicate<Message> { message in
        message.recipients.contains {
            $0.firstName == message.sender.firstName
        }
    }
```

[PredicateCodableConfiguration](https://developer.apple.com/documentation/foundation/predicatecodableconfiguration): `Predicate`는 *encode 와 decode*도 가능하다.

