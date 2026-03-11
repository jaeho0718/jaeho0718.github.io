---
title: "SwiftUI State Management 정리"
date: 2026-02-20
categories: [Framework]
pinned: true
excerpt: "SwiftUI의 @State, @ObservedObject, @EnvironmentObject 등 상태 관리 프로퍼티 래퍼를 비교 정리합니다."
image: ""
---

## Overview

SwiftUI는 여러 프로퍼티 래퍼를 통해 상태를 관리합니다. 각각의 용도와 차이점을 정리합니다.

## @State

`@State`는 뷰가 소유하는 간단한 값 타입 상태에 사용합니다.

```swift
struct CounterView: View {
    @State private var count = 0

    var body: some View {
        Button("Count: \(count)") {
            count += 1
        }
    }
}
```

## @ObservedObject

외부에서 주입받는 참조 타입 객체를 관찰할 때 사용합니다. `ObservableObject` 프로토콜을 준수하는 클래스와 함께 씁니다.

```swift
class UserSettings: ObservableObject {
    @Published var username = ""
}

struct SettingsView: View {
    @ObservedObject var settings: UserSettings

    var body: some View {
        TextField("Username", text: $settings.username)
    }
}
```

## @EnvironmentObject

뷰 계층 전체에서 공유되는 객체입니다. 부모 뷰에서 `.environmentObject()`로 주입합니다.

## 비교표

| 프로퍼티 래퍼 | 소유권 | 타입 | 범위 |
|:---|:---|:---|:---|
| `@State` | 뷰 소유 | Value | 단일 뷰 |
| `@ObservedObject` | 외부 주입 | Reference | 공유 |
| `@EnvironmentObject` | 환경 주입 | Reference | 서브트리 |
| `@StateObject` | 뷰 소유 | Reference | 생명주기 연결 |
