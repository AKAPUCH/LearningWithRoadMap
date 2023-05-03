# ios 로드맵

<details>
<summary>2023 ios 개발 로드맵 이미지</summary>
<div markdown="2">

<img src="https://user-images.githubusercontent.com/116094622/226232412-fc705ced-f70b-4008-b1bb-80061bd5482b.jpg" alt="로드맵">

</div>
</details>

## 항목(선택적 항목은 블록처리)
### 기본기
#### Xcode 사용법 & 플레이그라운드
#### 문법
- swift & 함수형 프로그래밍
- [objective-c & 객체지향 프로그래밍](https://github.com/AKAPUCH/LearningWithRoadMap/tree/main/ios/objective-c)
- `objective-c++`
### 공통 주제
#### HIG
#### ios 기술
- [multi-touch-event-handling](https://github.com/AKAPUCH/LearningWithRoadMap/tree/main/ios/commonSubject/iosSkills/multi-touch-event-handling)
- [app life cycle](https://github.com/AKAPUCH/LearningWithRoadMap/tree/main/ios/commonSubject/iosSkills/multi-touch-event-handling)
- app architect
- view-viewcontroller programming & AutoLayout
#### 코코아 디자인 패턴
- MVC 패턴
- 싱글톤 패턴
- Delegate 패턴
- responder-chain 패턴
- observer 패턴
#### 네트워크 프로그래밍
- restful-apis
- `TCP/IP socket apis`
### 주제별 Deep-dive
#### Swift
-  프로토콜 지향 프로그래밍
	- Value Semantics
	- Generics
- 동시성 프로그래밍
	- DispatchQueue
- 고급 디자인 패턴
	- VIPER
	- [MVVM](https://github.com/AKAPUCH/LearningWithRoadMap/tree/main/ios/DeepDive/Swift/DesignPattern/MVVM)
	- ReactorKit
#### Obejctive-C
- Manual Memory Management(MRC, ARC)
- 동시성 프로그래밍
	- 블록
	- GCD Queue
	- `GCD Event`
- `Runtime`
#### 시스템 프레임워크
- Swift Standard
- Swift Foundation
- `Core Foundation`
- Cocoa Touch
- Core Data
#### 반응형 프로그래밍
- Combine
	- SWIFTUI
	- VIPER 적용?
- RXSwift
  - MVVM 적용
- ReactiveCocoa
#### 데이터 영속성
- Core Data & `Sqlite`
- Realm
- 직렬화
	- Plist
	- JSON
	- 키체인
- KeyedArchiver
- `Cloud`
	- iCloud
	- FireBase
#### [프로젝트 & 워크스페이스 관리](https://github.com/AKAPUCH/LearningWithRoadMap/tree/main/ios/DeepDive/Project%26Workspace%20Manage)
- Build Config
- `Scheme`
- Target
- 패키지 매니저
	- Swift Package Manager(SPM)
	- [CocoaPods](https://github.com/AKAPUCH/LearningWithRoadMap/tree/main/ios/DeepDive/Project%26Workspace%20Manage/CocoaPods)
	- `Carthage`
#### 테스트
- Instruments
	- Allocations
	- Leaks
	- Time Profile
	- `Network`
	- `Activity`
	- `Energy`
	- `Layout`
	- `System Trace`
- XCTest
	- TDD
	- Mocks
	- Quick/Nimble
- UITest
- Code Coverage
#### 디버깅
- [LLDB](https://github.com/AKAPUCH/LearningWithRoadMap/tree/main/ios/Debugging/LLDB)
- Break-Pointer
- `Gauges`
- `Visual Debugging & Sanitizer`
- `Diagnostics`

### 빌드
#### CI
- `Jenkins`
- Fastlane
- bitrise
- Travis
- Xcode Server
#### 분석 도구
- TestFlight
- Crashlytics & Fabric
- GA
- UserHabit
#### 앱스토어
- 리뷰 가이드라인
- iTunes Connect
- Lucky Reviewer
