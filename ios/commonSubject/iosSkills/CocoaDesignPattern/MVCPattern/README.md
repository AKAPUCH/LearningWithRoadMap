# MVC 패턴
## 참고 문헌
- [kodeco](https://www.kodeco.com/1000705-model-view-controller-mvc-in-ios-a-modern-approach)
## 기본 정의
![mvc](https://koenig-media.raywenderlich.com/uploads/2019/01/01-MVC-Diagram.png)

- 앱의 구조를 model-controller-view로 나누어 개발하는 방식입니다.
- controller만이 model, view를 모두 알고 있고 model과 view는 서로 소통하지 않습니다.
## 계층별 특징
### M(Model)
- 데이터와 관련된 구조체, 클래스들이 존재하는 계층입니다.
- 데이터를 이용한 비즈니스 로직들이 구현되고 이 때문에 테스트에 자주 사용됩니다.
- 주로 구현되는 코드들
  - 네트워크 통신 코드 : 오류처리,응답과 같은 여러 네트워크 로직은 하나의 클래스로 처리하는 것 권장
  - 영속성 관리 코드 : 데이터베이스, Core Data와 같은 데이터 저장소에 트랜잭션하는 코드들
  - encoding/decoding : JSON <-> 구조체 간 변환하는 코드
  - 관리자 객체 : 여러 클래스에서 공통적으로 사용하는 로직들을 하나의 '관리자'객체를 통해 구현
  - dataSource, Delegate : 사용자 로직이 많은 경우 컨트롤러에서 구현하나 종종 모델로도 대신함
  - 기타 : 공통적으로 재사용하는 상수, 이미 구현된 클래스나 프로토콜의 extension들

### V(View)
- 사용자가 앱에 상호작용할 수 있는 계층입니다.
- View는 Model 계층과 상호작용하거나 비즈니스 로직이 포함되서는 안됩니다.
- 재사용가능하도록 만드는 것이 권장됩니다.
- 테스트 시 UI전환, 특정 속성이 존재하는 UI요소, UI 상호작용 등을 포함합니다.
- 주로 구현되는 코드들 : 모두 화면(UI)과 관련된 것들입니다.
  - UIView 및 관련 객체
  - UIKit/AppKit 관련 클래스
  - Core Animation, Core Graphics
  
### C(Controller)
- 앱의 의사결정을 주도하는 계층으로서 View와 Model 사이에서 소통합니다.
- 도메인 관련 로직이 포함될 수 있어 재사용성이 낮습니다.
- 테스트에는 적합하지 않습니다.
- 주로 구현되는 코드들
  - 현재 작업들의 접근 우선순위 결정
  - 앱의 새로고침 주기 결정
  - 전환시 UI 결정
  - 앱의 background 작업 결정
  - 사용자가 View에 상호작용 시 앱의 동작 결정
