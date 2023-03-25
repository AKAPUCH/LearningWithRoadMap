# Develop Lighthouse
<img src="https://user-images.githubusercontent.com/116094622/226248427-13d4c149-26a6-4cb1-b7b5-5c48f91372e8.png" alt="EyeOfSouron" style="width:50%;">

    개발의 왕도는 없지만, 학습 방향이 정해지지 않아 방황하거나 체계적인 계획을 통해 학습하고 싶은 사람을 위한 길잡이이자 등대입니다.


<details>
<summary>ios 로드맵</summary>
<div markdown="1">

[원본 : 코드스쿼드 고드름님 레포](https://github.com/godrm/mobile-developer-roadmap)	
	
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
- multi-touch-event-handling
- app life cycle
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
	- MVVM
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
#### 프로젝트 & 워크스페이스 관리
- Build Config
- `Scheme`
- Target
- 패키지 매니저
	- Swift Package Manager(SPM)
	- CocoaPods
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
- LLDB
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

</div>
</details>



<details>
<summary>swift 학습 로드맵</summary>
<div markdown="1">

<details>
<summary>swift 학습 로드맵 이미지</summary>
<div markdown="2">

<img src="https://user-images.githubusercontent.com/116094622/227720903-2e07cbe2-1ed4-4f37-8ce7-d5e067d59dea.png" alt="로드맵">

</div>
</details>

# 항목
## Prodecural Presentation
### 기본 연산자
- ternary, binary, unary
- Combinations
- assignment, arithmetic, Comparison, Range, Logical
- Advanced Operators
### 흐름 제어
- While, For-In 반복문
- guard문
- switch-case, If-else
- #Availability
### 함수
- Opaque Types
- 파라미터와 반환 값
- Nested Functions
- Function Types
- In-Out
### 클로저
- Currying
- Trailing Closures
- Expression
- Auto closures
- Escaping Closures
- Capture 현상
### 함수형 프로그래밍
- 고차함수
- 일급 합수
- 불변 값(Immutable Values)
### Extensions
- 생성자
- 메서드
- 속성
- Nested Type
- 서브스크립트
- Confirm Protocol
### Error Handling
- rethrows, throws, do-catch, Error Protocol
### 접근 제어
- Private, File private, Internal, Public, Open
### Objective-c와 연계
- Migration, Import From/to
- InterOperability
- Bridge Header

## Data Presentation
- 변수와 상수
- 주석
### 원시 타입
- Integer, Float/Double
	- Numeric Literals
	- Conversion
- Boolean
- String/Chracter
	- 유니코드
	- SubString, Indices
- Optional
	- nil
	- Optional binding
	- Optional chaining
	- IUO
- Tuple
### 컬렉션
- Array(배열)
- Set(집합)
- Dictionary
### 객체 타입
- value type(enum , struct)
- reference type(Class)
- property
	- 저장 property
	- 연산 property
	- 속성 감시자
	- Wrapper
	- 타입 property
- 메서드
	- 인스턴스/타입 메서드
- 서브스크립트
	- Options
- 생성자(Initialization)
	- Delegation
	- Two-Phase
	- Failable
	- Required
- 소멸자(DeInitialization)
- 상속
	- 자손 클래스
	- Overriding
### OOP
### 프로토콜
- POP(Protocol Oriented Programming) : 다중 상속..
- 프로토콜 요구사항
- 타입으로서의 프로토콜
- Composition
- 메서드 요구사항
- Delegation
- Optional
- 생성자 요구사항
- 상속
- 기본 구현
### Generic
- Association Type
- Generic 함수/타입/서브스크립트
- 타입 파라미터/Constraints
- Generic WHere Clause
### 메모리
#### ARC
- 강한 참조, 약한 참조
	- 참조 사이클
- 비소유 참조(Unowned Reference)
#### 접근
- Layout
- UnsafePointer
### 디버깅
- Assertions
- Preconditions

</div>
</details>


<details>
<summary>컴퓨터공학(CS) 로드맵</summary>
<div markdown="1">

### [원본 링크](https://roadmap.sh/computer-science)

<details>
<summary>원본 이미지 보기</summary>
<div markdown="2">

<img src="https://raw.githubusercontent.com/kamranahmedse/developer-roadmap/master/public/roadmaps/computer-science.png" alt="로드맵" style="width:50%; height: 50%">

</div>
</details>

### 언어(필자는 Swift)
### 자료구조
- 배열
- 그래프
	- Directed 그래프
	- Undirected 그래프
	- Spanning Tree
	- 그래프 표현 : Adjacency Matrix, Adjacency List
- 힙 
- 링크드리스트
- 스택
- 큐
- 해쉬테이블
- 트리
	- 이진트리
	- 이진탐색트리
	- Full 이진 트리
	- Complete 이진 트리
	- Balanced 트리
	- Unbalanced 트리
### 시간복잡도 표기법
- Big O 표기법
- Big 세타 표기법
- 빅 오메가 표기법
### 공통 알고리즘
- 정렬
	- 버블 정렬
	- 선택 정렬
	- 삽입 정렬
	- 힙 정렬
	- 퀵 소트
	- 병합 정렬
- 그래프
	- BFS
	- DFS
	- 벨만포드
	- 다익스트라
	- A* 알고리즘
- 그리디
	- 다익스트라
	- Huffman Coding
	- Kruskal's Algorithm
	- Ford-Fulkerson Algorithm
	- Prim's Algorithm
- 트리
	- Pre-Order 순회
	- In-Order 순회
	- Post-Order Traversal
	- 트리 BFS
	- 트리 DFS
- 백트래킹
	- Finding Hamiltonian Paths
	- Solving N Queen Problem
	- Maze Solving Problem
	- The Knight's TOur Problem
	- 라빈-카프 알고리즘
- 재귀
	- Tail Recursion
	- Non-Tail Recursion
- 탐색
	- 이진탐색
	- 선형탐색
- 캐시
	- LRU Cache
	- LFU Cache
	- MFU Cache
### 문자열 탐색 및 다루기
- 텍스트 탐색 패턴
- Suffix Arrays
- 부분문자열 탐색
	- 브루트포스 탐색
	- KMP
	- 보어-무어
	- 라빈 카프
### Bitwise Operators
### Floating Point Numbers
### Endianess
- Big Endian
- Little Endian
### 문자 인코딩
- 유니코드
- ASCII(아스키코드)
### 공통 UML 다이어그램
- 클래스 다이어그램
- 유스케이스 다이어그램
- 액티비티 다이어그램
- stateMachine 다이어그램
- 시퀀스 다이어그램
### 디자인패턴
- GOF 디자인 패턴
- 아키텍쳐 패턴
- 의존성 주입
- Null 객체 패턴
- Type 객체 패턴
### 기본 수학 지식
- 확률
- 조합론
### Complexity Classes
- P, NP, CO-NP, HP Hard
- NP Complete
- P = NP
- TSP 문제
- 배낭문제(냅섹)
- 최장경로 문제
### Tries
### Balanced Search Trees
- 2-3-4 Trees
- K-ary / M-ary Tree
- B- Tree
### 시스템 디자인
- Horizonal vs Vertical Scaling
- Load Balancing
- 클러스터링, 캐싱
- CDN, 프록시
- CAP Theorem, Queues
- 아키텍쳐 스타일
- REST
- GraphQL
- gRPC
- Cloud Design Patterns
- Long/ Short Polling
- Web Sockets, SSE
### 네트워킹
- OSI Model
- TCP / IP Model
- DNS, HTTP
- TLS & HTTPS
- Sockets
### 보안
- Public Key Cryptography
- Hashing / Encryption / Encoding
- Hashing Algorithms
- OWASP Top 10
### 컴퓨터 동작 원리
- CPU가 어떻게 프로그램을 실행할까
- 컴퓨터는 어떻게 연산을 할까
- 레지스터, 램
- Instructions, 프로그램
- CPU 캐시
### 프로세스와 쓰레드
- Process Forking
- 메모리 관리
- Lock / Mutex / Semaphore
- Concurrency in Multiple cores
- Scheduling Algorithms
- CPU Interrupts
- 프로세스 vs 쓰레드
### K-D Trees
### skip lists
###  데이터베이스
- SQL vs NOSQL
- Normalization / Denormalization
- Entity-Relationship Model
- DDL/DML/DQL/DCL
- Locking, Transactions
- ACID Model, BASE Model
- CAP Theorem, PACELC
- Indexes, Views
- Stored Procedures
- Database Federation
- Replication, Sharding
</div>
</details>
