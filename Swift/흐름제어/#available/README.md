# #available

- #available은 Bool변수처럼 사용되어 if, guard 등을 통해 분기처리로 작업을 처리할 수 있게 해줍니다.

```swift
 if #available(iOS 12, *) {
  //ios 12이상에서의 동작 구현
} else {
// 그 미만 버전들...
}
```

### @available과의 차이?
- @available은 함수 또는 클래스 가장 상단에 표기하여 가능한 버전, 플랫폼 등을 표기하여 개별적으로 적용할 수 있는 attribute입니다.

 

### 참고 문헌
- [ZEDDIOS님 블로그](https://zeddios.tistory.com/647)
- [애플 공식문서 Swift- attribute](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/attributes/#available)
